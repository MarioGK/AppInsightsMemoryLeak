FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["AspNet6/AspNet6.csproj", "AspNet6/"]
RUN dotnet restore "AspNet6/AspNet6.csproj"
COPY . .
WORKDIR "/src/AspNet6"
RUN dotnet build "AspNet6.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "AspNet6.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspNet6.dll"]
