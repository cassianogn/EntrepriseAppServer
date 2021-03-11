#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/services/EntApp.Api.Indenty/EntApp.Api.Indenty.csproj", "src/services/EntApp.Api.Indenty/"]
RUN dotnet restore "src/services/EntApp.Api.Indenty/EntApp.Api.Indenty.csproj"
COPY . .
WORKDIR "/src/src/services/EntApp.Api.Indenty"
RUN dotnet build "EntApp.Api.Indenty.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EntApp.Api.Indenty.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EntApp.Api.Indenty.dll"]