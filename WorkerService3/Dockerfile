#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["WorkerService3/WorkerService3.csproj", "WorkerService3/"]
COPY ["UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Configuration/Opc.Ua.Configuration.csproj", "UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Configuration/"]
COPY ["UA-.NETStandard-1.4.365.23/Stack/Opc.Ua.Core/Opc.Ua.Core.csproj", "UA-.NETStandard-1.4.365.23/Stack/Opc.Ua.Core/"]
COPY ["UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Security.Certificates/Opc.Ua.Security.Certificates.csproj", "UA-.NETStandard-1.4.365.23/Libraries/Opc.Ua.Security.Certificates/"]
RUN dotnet restore "WorkerService3/WorkerService3.csproj"
COPY . .
WORKDIR "/src/WorkerService3"
RUN dotnet build "WorkerService3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WorkerService3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WorkerService3.dll"]