FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["AspNet8AppInsights/AspNet6AppInsights.csproj", "AspNet6AppInsights/"]
RUN dotnet restore "AspNet6AppInsights/AspNet6AppInsights.csproj"
COPY . .
WORKDIR "/src/AspNet6AppInsights"
RUN dotnet build "AspNet6AppInsights.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "AspNet6AppInsights.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspNet6AppInsights.dll"]
