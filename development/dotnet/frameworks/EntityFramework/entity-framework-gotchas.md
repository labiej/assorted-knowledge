# Entity framework gotchas

## Eager loading

Foreign keys are not loaded by default. Using eager loading it is possible to include a FK relation with a single query. Consider the following basic model (ignoring the fact that each level of sub categories needs an extra table).

```cs
class Category : Entity 
{
	[Key]	
	public int Id { get; set; }

	[Required]
    public string Name { get; set; }
	
	public virtual ICollection<SubCategory> SubCategories { get; set; }
}

class SubCategory : Entity
{
	[Key, Column(Order = 1), ForeignKey("Category")]
	public int CategoryId { get; set; }
	
	[Key, Column(Order = 2)]
	public int Id { get; set; }

	[Required]
    public string Name { get; set; }
	
	public Category Parent { get; set; }
}
```

A common query could be the following inside a LoadFullCategory method

```cs
var dbCategory = context.Categories.Where(cat => cat.Id == categoryId).FirstOrDefault();

var subCategories = dbCategory.SubCategories.ToList();
```

This will execute 2 queries, the first query for loading the category. The second query is hidden by Entity framework and will execute when the SubCategories property is evaluated.

Sometimes it is prudent to use eager-loading. In this case the generated query will include all subcategories in a single round-trip to the database (the query cost increases but round-trips are avoided).

```cs
var eagerLoaded = context.Categories.Include(cat => cat.SubCategories)
	.Where(cat => cat.Id == categoryId)
	.FirstOrDefault();
```

Eager loading is easily 'broken' in the sense that the data is no longer loaded within the same query when performing certain types of queries. A common exampe is when joining. While it is not too common for simple databases it will bite you in the ass you if you don't pay attention.