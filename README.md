# Chucker.Blazor.BuildTasks.GitHashedIndexHtml

## How to use

In your `index.html`, ensure that assets that may change have their URLs
suffixed by the template string in their URL. For example, instead of:

```html
<link rel="stylesheet" href="css/app.css" />
```

, you should use:

```html
<link rel="stylesheet" href="css/app.css?GitHashedTemplate" />
```

In your Blazor app's `csproj`, add a new target, and hook it to run after
`_ProcessPublishFilesForBlazor`:

```xml
<Target Name="AddGitHashesToIndexHtml" AfterTargets="_ProcessPublishFilesForBlazor">
    <GitHashedIndexHtml />
</Target>
```

Now, when _publishing_ (not when building!), the publish output will have an
`index.html` with those template strings replaced with a seven-character git
hash, for example:

```html
<link rel="stylesheet" href="css/app.css?abcd012" />
```

