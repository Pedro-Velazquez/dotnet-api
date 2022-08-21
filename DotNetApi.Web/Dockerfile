FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DotNetApi.Web/DotNetApi.Web.csproj", "DotNetApi.Web/"]
RUN dotnet restore "DotNetApi.Web/DotNetApi.Web.csproj"
COPY . .
WORKDIR "/src/DotNetApi.Web"
RUN dotnet build "DotNetApi.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetApi.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetApi.Web.dll"]
