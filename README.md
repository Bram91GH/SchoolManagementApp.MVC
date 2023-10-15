## Project Controller

### Create a New Project

#### GET: Project/Create

This method handles the HTTP GET request to create a new project.

##### Parameters

None

##### Returns

- `IActionResult`: Returns a view to create a new project.

##### Usage

```csharp
public IActionResult Create()
{
    CreateSelectLists();
    return View();
}
```

#### POST: Project/Create

This method handles the HTTP POST request to create a new project. It protects against overposting attacks by binding specific column properties.

##### Parameters

- `project` (`Project`): The project object to be created.
- `ClientId` (`int`): The ID of the client associated with the project.

##### Returns

- `Task<IActionResult>`: Returns an asynchronous task which resolves to a redirect to the details view of the created project if successful, or a view with validation errors if unsuccessful.

##### Usage

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Create([Bind("Id,ClientId,ContactId,ExpertiseId,ProjectName,ProjectDescription,ProjectDeadline,ProjectStatus")] Project project, int ClientId)
{
    if (ModelState.IsValid)
    {
        // Assign the selected ClientId
        project.ClientId = ClientId;

        _context.Add(project);
        await _context.SaveChangesAsync();
        return RedirectToAction(nameof(Details), new { id = project.Id });
    }

    CreateSelectLists();
    return View(project);
}
```

For more information on protecting against overposting attacks, see [this link](http://go.microsoft.com/fwlink/?LinkId=317598).

---

### Notes

- The `CreateSelectLists` method is assumed to be defined elsewhere in the controller to populate select lists used in the view.

---

This documentation provides an overview of the `Create` actions in the `Project` controller, including their purpose, parameters, return types, and usage. It also includes a note regarding the assumed existence of the `CreateSelectLists` method.
