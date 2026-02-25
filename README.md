# SLPE.Blazor.DiffViewer

A Blazor component for displaying HTML diff output with highlighted insertions/deletions and a clean-view toggle. Pure presentation component with no service dependencies.

## Installation

Add a project reference (or NuGet package when published):

```xml
<ProjectReference Include="path/to/SLPE.Blazor.DiffViewer.csproj" />
```

Add the CSS stylesheet to your `App.razor` (or `_Host.cshtml`):

```html
<link rel="stylesheet" href="_content/SLPE.Blazor.DiffViewer/css/diff-viewer.css" />
```

Add the namespace to your `_Imports.razor`:

```razor
@using SLPE.Blazor.DiffViewer
```

## Usage

The component accepts pre-computed diff HTML (e.g. from [HtmlDiff.NET](https://www.nuget.org/packages/HtmlDiff)) and displays it with highlighted changes.

```razor
<DiffViewer DiffHtml="@diffOutput"
            CleanHtml="@newerVersionHtml"
            ContentClass="prose max-w-none" />

@code {
    private string diffOutput = "<p>Hello <del>world</del><ins>everyone</ins></p>";
    private string newerVersionHtml = "<p>Hello everyone</p>";
}
```

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `DiffHtml` | `string` | `""` | **Required.** The HTML diff output containing `<ins>` and `<del>` tags |
| `CleanHtml` | `string` | `""` | The newer version's raw HTML for "Clean view" mode |
| `ShowToggle` | `bool` | `true` | Whether to show the "Show changes" / "Clean view" toggle buttons |
| `ShowLegend` | `bool` | `true` | Whether to show the Added/Removed legend |
| `ShowChangesInitially` | `bool` | `true` | Which view to show first (`true` = diff, `false` = clean) |
| `ContentClass` | `string` | `""` | Additional CSS classes for the diff content container |

## Theming

All colours use CSS custom properties. Override them in your application CSS:

```css
:root {
    --diff-added-bg: #d1fae5;
    --diff-added-text: #065f46;
    --diff-removed-bg: #fee2e2;
    --diff-removed-text: #991b1b;
    --diff-toggle-bg: #e5e7eb;
    --diff-toggle-text: #374151;
    --diff-toggle-active-bg: #00173b;
    --diff-toggle-active-text: #ffffff;
}
```

### Dark mode

The component responds to a `.dark` ancestor class (e.g. on `<html class="dark">`). Dark-mode variables are defined under `.dark { ... }` in the default stylesheet.

## Generating diff HTML

This component is a pure presentation layer. Use a library like [HtmlDiff.NET](https://www.nuget.org/packages/HtmlDiff) to generate the diff HTML:

```csharp
var diff = new HtmlDiff.HtmlDiff(olderHtml, newerHtml);
var diffHtml = diff.Build();
```

## License

MIT
