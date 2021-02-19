# Bug reproduction

Freshly scaffolded .NET Core 3.1 Worker project, including UA-.NETStandard-1.4.365.23 full source code (freshly unzipped).

Only added ApplicationInstance initialization in Worker.ExecuteAsync.

Project builds and runs successfully in VS2019 debug under Windows.

Docker build error, using VS2019-generated `Dockerfile` and included `docker-compose.yml`:

```PowerShell
PS C:\Source\Repos\WorkerService3> docker-compose build
Building worker
Step 1/18 : FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
 ---> aeda02cc2c98
Step 2/18 : WORKDIR /app
 ---> Using cache
 ---> 6e41bf397776

Step 3/18 : FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
 ---> ec3ca8a1472c
Step 4/18 : WORKDIR /src
 ---> Using cache
 ---> 57ede842e36a
Step 5/18 : COPY ["WorkerService3/WorkerService3.csproj", "WorkerService3/"]
 ---> 3df132dca8cd
Step 6/18 : COPY ["UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Configuration/Opc.Ua.Configuration.csproj", "UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Configuration/"]
 ---> 193ddd1088a0
Step 7/18 : COPY ["UA-.NETStandard-1.4.365.23/Stack/Opc.Ua.Core/Opc.Ua.Core.csproj", "UA-.NETStandard-1.4.365.23/Stack/Opc.Ua.Core/"]
 ---> fca10e008bd2
Step 8/18 : COPY ["UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Security.Certificates/Opc.Ua.Security.Certificates.csproj", "UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Security.Certificates/"]
 ---> 9db2d8b8ebff
Step 9/18 : RUN dotnet restore "WorkerService3/WorkerService3.csproj"
 ---> Running in 45ac56479a19
  Determining projects to restore...
/usr/share/dotnet/sdk/3.1.406/NuGet.targets(128,5): error : Value cannot be null. (Parameter 'folderName') [/src/WorkerService3/WorkerService3.csproj]
ERROR: Service 'worker' failed to build : The command '/bin/sh -c dotnet restore "WorkerService3/WorkerService3.csproj"' returned a non-zero code: 1
```
