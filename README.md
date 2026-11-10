# Doctor Appointment Hub — Backend

An ASP.NET Core API supporting a doctor appointment management application. The backend models patients, doctors, appointments, and administrators, connecting account workflows and scheduling operations to SQL Server persistence.

## Application domains

- **Patients:** registration, authentication, account retrieval, and account updates.
- **Doctors:** creation, lookup, listing, updates, and deletion through administrative workflows.
- **Appointments:** booking, retrieval by patient or doctor, listing, updates, and deletion.
- **Administrators:** authentication, account management, and online-user information.

## Architecture

```text
HTTP request → Controller → Repository → Entity Framework Core → SQL Server
                    |
          Logged-in account services
```

`ServerApp/Controllers` defines explicit `api/admin`, `api/patient`, `api/doctor`, and `api/appointment` routes. `Repository` classes encapsulate data operations, while `Model/DatabaseContext.cs` maps the application entities through Entity Framework Core. `Service/LoggedInAdmins` and `Service/LoggedInPatients` maintain the application's active-account collections. The `Migrations/` directory records the database schema.

## Representative endpoints

| Operation | Route |
| --- | --- |
| Patient sign-in | `POST /api/patient/authenticate` |
| Patient registration | `POST /api/patient/add` |
| Doctor listing | `GET /api/doctor/getAll` |
| Appointment booking | `POST /api/appointment/add` |
| Patient appointments | `GET /api/appointment/getByPatientId` |
| Administrator sign-in | `POST /api/admin/authenticate` |

Request bodies and query parameters are defined in the corresponding controller methods.

## Development setup

The project targets **.NET Core 2.0** and references ASP.NET Core 2.0. Use a matching SDK and a SQL Server instance compatible with the connection configured in `DatabaseContext`. Apply the included Entity Framework migrations using the matching tooling.

```bash
dotnet restore ServerApp.sln
dotnet run --project ServerApp/ServerApp.csproj
```

For the companion Angular client's default connection, expose the API at `http://localhost:5002`. The backend configures cross-origin requests in `Startup.cs`.

## Technical focus

The project demonstrates a layered API, entity-based persistence, schema migrations, dependency-injected account services, and coordinated patient/administrator workflows.
