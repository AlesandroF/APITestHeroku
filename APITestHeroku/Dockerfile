FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["APITestHeroku/APITestHeroku.csproj", "APITestHeroku/"]
RUN dotnet restore "APITestHeroku/APITestHeroku.csproj"
COPY . .
WORKDIR "/src/APITestHeroku"
RUN dotnet build "APITestHeroku.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "APITestHeroku.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "APITestHeroku.dll"]