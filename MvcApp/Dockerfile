FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-stretch-slim AS base
WORKDIR /app
EXPOSE 3317
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-stretch AS build
WORKDIR /src
COPY ["/MvcApp.csproj", "MvcApp/"]
RUN dotnet restore "MvcApp/MvcApp.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "MvcApp.csproj" -c Release -o /app/build --no-restore

FROM build AS publish
RUN dotnet publish "MvcApp.csproj" -c Release -o /app --no-restore

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MvcApp.dll"]