FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MongoDbPcf.Web/MongoDbPcf.Web.csproj", "MongoDbPcf.Web/"]
RUN dotnet restore "MongoDbPcf.Web/MongoDbPcf.Web.csproj"
COPY . .
WORKDIR "/src/MongoDbPcf.Web"
RUN dotnet build "MongoDbPcf.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MongoDbPcf.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MongoDbPcf.Web.dll"]
