# 🔗 How to bind MySQL database to a Pivot Table

A quick start project for connecting a MySQL database to a Syncfusion Pivot Table. This repository includes a Web API Controller ([MyWebService](./MyWebService/)) for retrieving data from a MySQL database, as well as quick start samples in the [TypeScript](./Typescript/), [JavaScript](./Javascript/), [Angular](./Angular/), [React](./React/), [VUE](./VUE/), ASP.NET [Core](./Core/), [Blazor](./Blazor/) and [MVC](./MVC/) platforms that display the retrieved data in a Syncfusion Pivot Table.

---

## 📚 Table of Contents

- [🔎 Project Overview](#-project-overview)
- [🚀 Quick Start](#-quick-start)
- [✨ Key Features](#-key-features)
- [🛠️ Supported Technologies & Requirements](#️-supported-platforms--dependencies)
- [⚙️ Installation & Setup (quick)](#-installation-setup)
- [🧩 Quick Code Samples](#-quick-code-samples)
- [🏗️ Project Structure](#-project-structure)
- [❓ Troubleshooting & FAQ](troubleshooting--FAQ)
- [🧪 Testing & CI](#-testing--ci)
- [🤝 Contributing](#-contributing)
- [📜 License & Support](#-license--support)
---

## 🔎 Project Overview
This repository shows how to expose MySQL query results via a Web API and bind the returned JSON to a Syncfusion Pivot Table (PivotView). It includes server-side (.NET) and client-side examples (JS/TS/Angular/React/Vue, plus ASP.NET Core, Blazor, MVC).

Real-world uses:
- Web BI dashboards
- Ad-hoc reporting and analytics
- Rapid prototyping of pivot-based UI

---

## 🚀 Quick Start

Prerequisites
- MySQL server with sample data
- .NET SDK 6.0+ (or matching project target)
- Node.js (for front-end samples)
- Syncfusion NuGet/npm packages

Run the Web API (`MyWebService`)

```bash
cd MyWebService
dotnet restore
dotnet run
# API runs on the configured port (see Properties/launchSettings.json)
```

Run a front-end sample (choose one):

TypeScript
```bash
cd Typescript/pivot-table
npm install
npm start
```

Angular
```bash
cd Angular/pivot-table
npm install
npm start
```

React
```bash
cd React/pivot-table
npm install
npm start
```

Vue
```bash
cd VUE/pivot-table
npm install
npm run dev
```

First success: Open the front-end sample URL (e.g., http://localhost:3000 or http://localhost:4200) and confirm the PivotView loads rows from the running Web API.

---

## ✨ Key Features
- Web API sample that returns MySQL query results as JSON (server-side .NET)
- Client demos for JavaScript, TypeScript, Angular, React, Vue
- ASP.NET Core, Blazor, and MVC integration examples
- appsettings.json example for secure DB connection configuration
- Minimal, copy-paste-ready snippets to initialize Syncfusion PivotView
- Framework-agnostic architecture for easy reuse

---

## 🛠️ Supported Technologies & Requirements
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

## ⚙️ Installation & Setup (quick)
Prereqs:
- MySQL server with sample data
- .NET SDK 6.0+ (or matching project target)
- Node.js 14+
- Syncfusion NuGet/npm packages

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

## 🧪 Testing & CI

- Add GitHub Actions to build the Web API and optionally run front-end builds per sample. Suggested jobs:
	- `dotnet restore` / `dotnet build` / `dotnet test`
	- `npm ci` / `npm run build` for front-end samples

---

## 🤝 Contributing

Contributions welcome. Suggested workflow:
1. Fork and create a branch `feature/<desc>`
2. Run the Web API locally and test sample clients
3. Open a PR with description, screenshots, and testing steps

## 📜 License & Support

This is a **commercial product** subject to the Syncfusion End User License Agreement (EULA).

**Free Community License** is available for qualifying users/organizations:  
- Annual gross revenue < $1 million USD  
- 5 or fewer total developers  
- 10 or fewer total employees  

The community license allows free use in both internal and commercial applications under these conditions.  
No registration or approval is required — just comply with the terms.

**Paid Licenses** are required for:  
- Larger organizations  
- Teams exceeding the community license limits  
- Priority support, custom patches, or on-premise deployment options  

Purchase options and pricing: https://www.syncfusion.com/sales/products  
30-day free trial (full features, no credit card required): https://www.syncfusion.com/downloads/essential-js2  
Community License details & FAQ: https://www.syncfusion.com/products/communitylicense  
Full EULA: https://www.syncfusion.com/eula/es/

© 2026 Syncfusion, Inc. All Rights Reserved.

