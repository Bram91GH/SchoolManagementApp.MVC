---

## Project Controller

### Private Method for Object Relational Mapping

#### CreateSelectLists()

This private method is responsible for populating select lists used in the view for object relational mapping. It assigns the company and assisting contact to a new project.

##### Select Lists

- **Company Selection**:
  - Creates a select list to determine which company the project is for.
  - Assigns `ClientId` to the `Project` table `ClientId` column.
  - Associates the `Id` in the project table with the standalone project for routing to details pages.

```csharp
var clients = _context.Clients.Select(q => new
{
    ClientName = $"{q.CompanyName}",
    Id = q.Id
});
ViewData["CompanyId"] = new SelectList(clients, "Id", "ClientName");
```

- **Contact Selection**:
  - Creates a select list of contacts based on the `Id` of the client table.
  - Only contacts of the selected company appear in the select list.

```csharp
var contacts = _context.ClientContacts.Select(q => new
{
    ContactName = $"{q.FirstName} {q.LastName}",
    Id = q.Id
});
ViewData["ContactId"] = new SelectList(contacts, "Id", "ContactName");
```

- **Expertise Selection**:
  - Creates a select list of available expertises.

```csharp
var expertises = _context.Expertises.Select(q => new
{
    ExpertiseName = $"{q.Name}",
    Id = q.Id
});
ViewData["ExpertiseId"] = new SelectList(expertises, "Id", "ExpertiseName");
```

---

### Notes

- This method is used internally for object relational mapping within the `Project` controller. It populates select lists for company, contact, and expertise selection in the view.

---

This documentation provides an explanation of the `CreateSelectLists` method in the `Project` controller, including its purpose and the select lists it creates. The code snippets within the documentation demonstrate how each select list is generated.

Let me know if there's anything else you'd like to add or modify!
