# 🔗 How to bind MySQL database to a Pivot Table

A quick start project for connecting a MySQL database to a Syncfusion Pivot Table. This repository includes a Web API Controller ([MyWebService](./MyWebService/)) for retrieving data from a MySQL database, as well as quick start samples in the [TypeScript](./Typescript/), [JavaScript](./Javascript/), [Angular](./Angular/), [React](./React/), [VUE](./VUE/), ASP.NET [Core](./Core/), [Blazor](./Blazor/) and [MVC](./MVC/) platforms that display the retrieved data in a Syncfusion Pivot Table.

---

## 🚀 Bind MySQL to Syncfusion Pivot Table (Web Quick Start)

[![License](https://img.shields.io/github/license/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)](https://github.com/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table/blob/master/LICENSE) [![Last Updated](https://img.shields.io/github/last-commit/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)](https://github.com/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table/commits/master) [![Languages](https://img.shields.io/github/languages/top/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)](https://github.com/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)

A compact sample repository that demonstrates connecting MySQL → Web API → Syncfusion Pivot Table across multiple client frameworks. Last Updated: 2026-02-03

---

## 📚 Table of Contents
- 🔎 Quick overview
- ✨ Key features
- 🛠️ Supported technologies & requirements
- ⚙️ Installation & setup
- 🧩 Quick code samples
- 🏗️ Project structure
- ❓ Troubleshooting & FAQ
- 🤝 Contributing & license
- 🔎 SEO & metadata

---

## 🔎 Quick overview
This repository shows how to expose MySQL query results via a Web API and bind the returned JSON to a Syncfusion Pivot Table (PivotView). It includes server-side (.NET) and client-side examples (JS/TS/Angular/React/Vue, plus ASP.NET Core, Blazor, MVC).

Real-world uses:
- Web BI dashboards
- Ad-hoc reporting and analytics
- Rapid prototyping of pivot-based UI

---

## ✨ Key features
- Web API sample that returns MySQL query results as JSON (server-side .NET)
- Client demos for JavaScript, TypeScript, Angular, React, Vue
- ASP.NET Core, Blazor, and MVC integration examples
- appsettings.json example for secure DB connection configuration
- Minimal, copy-paste-ready snippets to initialize Syncfusion PivotView
- Framework-agnostic architecture for easy reuse

---

## 🛠️ Supported technologies & requirements
- Server: .NET (Core) — projects in MyWebService/*.csproj
- Database: MySQL
- Client: JavaScript / TypeScript; frameworks: Angular, React, Vue
- UI: Syncfusion EJ2 PivotView (Syncfusion packages required)
- Tooling: Node.js 14+, .NET SDK 6.0+ recommended
- Browsers: Modern browsers (Chrome, Edge, Firefox, Safari)

Suggested server deps:
- MySql.Data or MySqlConnector (for .NET)
- Microsoft.AspNetCore.App

Suggested client deps:
- @syncfusion/ej2-pivotview (or syncfusion ej2 equivalent)
- Build tools from each sample (npm, angular-cli, etc.)

---

## ⚙️ Installation & setup (quick)
Prereqs:
- MySQL server with sample data
- .NET SDK 6.0+ (or matching project target)
- Node.js 14+
- Syncfusion NuGet/npm packages (license/trial as required)

Steps:
1. Clone:
   ```bash
   git clone https://github.com/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table.git
   cd web-bind-MySQL-database-to-pivot-table
   ```
2. Configure DB (MyWebService/Controllers/PivotController.cs):
   ```csharp
   public dynamic GetMySQLResult()
    {
        MySqlConnection connection = new MySqlConnection("<Enter your valid connection string here>");
    }
   ```
3. Run Web API:
   ```bash
   cd MyWebService
   dotnet restore
   dotnet build
   dotnet run
   # API endpoints: http://localhost:5000/...
   ```
4. Launch a client example (Typescript):
   ```bash
   cd ../Typescript
   npm install
   npm start
   ```
5. Open the served client in your browser and confirm the PivotView loads.

---

## 🧩 Quick code samples

1) Minimal .NET Web API controller (Pivot data endpoint)
```csharp
// Controllers/PivotController.cs
// ...existing code...
[ApiController]
    [Route("[controller]")]
    public class PivotController : ControllerBase
    {
        [HttpGet(Name = "GetMySQLResult")]
        public object Get()
        {
            return JsonConvert.SerializeObject(GetMySQLResult());
        }

        public dynamic GetMySQLResult()
        {
            MySqlConnection connection = new MySqlConnection("<Enter your valid connection string here>");
            connection.Open();
            MySqlCommand command = new MySqlCommand("SELECT * FROM orders", connection);
            MySqlDataAdapter dataAdapter = new MySqlDataAdapter(command);
            DataTable dataTable = new DataTable();
            dataAdapter.Fill(dataTable);
            connection.Close();
            return dataTable;
        }
    }
// ...existing code...
```

2) appsettings.json example
```json
{
  "ConnectionStrings": {
    "MySqlConnection": "Server=localhost;Database=SalesDB;User=appuser;Password=secret;"
  }
}
```

3) Vanilla JS: fetch + PivotView init
```html
<!-- index.html -->
<div id="PivotView"></div>
<script src="https://cdn.syncfusion.com/ej2/32.1.19/dist/ej2.min.js"></script>
<script>
    var pivotObj = new ej.pivotview.PivotView({
    dataSourceSettings: {
        url: 'https://localhost:xxxx/...',
    },
    showFieldList: true,
    width: '100%',
    height: 350,
    });
    pivotObj.appendTo('#PivotView');
</script>
```

4) TypeScript snippet
```ts
// src/index.ts
import { PivotView } from '@syncfusion/ej2-pivotview';
let pivotTableObj: PivotView = new PivotView({
dataSourceSettings: {
  url: 'https://localhost:xxxx/....',
},
showFieldList: true,
width: '100%',
height: 350,
});
pivotTableObj.appendTo('#PivotTable');
```

---

## 🏗️ Project structure
- MyWebService/ — .NET Web API that queries MySQL
  - Controllers/ — API controllers (PivotDataController.cs)
  - appsettings.json — DB connection example
- Typescript/, Javascript/, Angular/, React/, VUE/ — client examples
- Core/, Blazor/, MVC/ — server-side web samples
- LICENSE, README.md — repo metadata

---

## ❓ Troubleshooting & FAQ
- Empty results: verify DB schema/table and connection string.
- CORS errors: enable CORS in Startup/Program for client origin.
- Pivot mapping issues: ensure JSON keys match dataSource field names.
- Syncfusion package errors: confirm correct package versions and license.

---

## 🤝 Contributing & license
Contributions: open issues or PRs; keep changes scoped and include reproduction steps.  
License: see LICENSE in repo root.

---

## 🔎 SEO & metadata
Meta description (<=160 chars): "Example showing how to bind a MySQL database to a Syncfusion Pivot Table via a Web API with JS/TS/Angular/React/Vue and .NET samples."  

Suggested primary keywords:
- Syncfusion Pivot Table
- MySQL Pivot binding
- PivotView MySQL example

Suggested GitHub topics:
syncfusion, pivot-table, mysql, dotnet, aspnet-core, javascript, typescript, angular, react, vue, blazor, mvc, pivotview, analytics, dashboard

Suggested README badges (example markdown):
```markdown
[![License](https://img.shields.io/github/license/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)](./LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)]()
[![Languages](https://img.shields.io/github/languages/top/SyncfusionExamples/web-bind-MySQL-database-to-pivot-table)]()
```

---

## 📌 Last updated
2026-02-03
