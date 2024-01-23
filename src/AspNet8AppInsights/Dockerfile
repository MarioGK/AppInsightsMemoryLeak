FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["AspNet8AppInsights/AspNet8AppInsights.csproj", "AspNet8AppInsights/"]
RUN dotnet restore "AspNet8AppInsights/AspNet8AppInsights.csproj"
COPY . .
WORKDIR "/src/AspNet8AppInsights"
RUN dotnet build "AspNet8AppInsights.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "AspNet8AppInsights.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspNet8AppInsights.dll"]
