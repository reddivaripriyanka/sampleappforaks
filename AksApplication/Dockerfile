FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["AksApplication/AksApplication.csproj", "AksApplication/"]
RUN dotnet restore "AksApplication/AksApplication.csproj"
COPY . .
WORKDIR "/src/AksApplication"
RUN dotnet build "AksApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AksApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AksApplication.dll"]