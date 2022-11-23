# Debugging angularjs

Tricks to use when attempting to debug an angularjs application.

## Inspect services

We can manually resolve services using the following snippet

```js
// Get a wrapped element to hook into the angular framework
const angularElement = angular.element(document.querySelector('html'));
// Next use the injector to get the dependency with name 'serviceName'
const service = angularElement.injector().get('serviceName');
```

Once we have the service we can simply use the service, check its interface etc. Particularly useful when testing API calls or when the need to inspect constants arises. 