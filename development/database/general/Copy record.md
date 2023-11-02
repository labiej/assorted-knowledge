# Copy a record
Sometimes it is useful to copy a record. For example when we need more data or when an intervention in a production database is needed.

To do this we can use values from a select query when inserting the record.
Consider a table with products for a shop system. A new vendor also starts selling  the same product at a different price.

```sql
INSERT INTO [Product] ([VendorId], [Name], [SKU], [Price])
SELECT
	12, [Name], [SKU], 15.23
FROM [Product]
WHERE [Id] =  719
```

Now suppose we have a slightly altered database structure where the price is extracted into a VendorProductPrice table (warning; this is not a very good model)

```sql
declare @products table (id int);

INSERT INTO [Product] ([VendorId], [Name], [SKU])
OUTPUT inserted.Id into @products
SELECT
	12, [Name], [SKU]
FROM [Product]
WHERE [Id] =  719

INSERT INTO [VendorProductPrice] ([VendorId], [ProductId], [Price])
SELECT
	12, id, 15.23
FROM @products
```

