#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
#FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
#FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS buil
WORKDIR /src
COPY DotnetCoreDocker/DotnetCoreDocker.csproj DotnetCoreDocker/
RUN dotnet restore "DotnetCoreDocker/DotnetCoreDocker.csproj"
COPY . .
WORKDIR "/src/DotnetCoreDocker"
RUN dotnet build "DotnetCoreDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotnetCoreDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotnetCoreDocker.dll"]
