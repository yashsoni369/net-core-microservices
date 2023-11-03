#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Dashboard.API/Dashboard.API.csproj", "Dashboard.API/"]
RUN dotnet restore "Dashboard.API/Dashboard.API.csproj"
COPY . .
WORKDIR "/src/Dashboard.API"
RUN dotnet build "Dashboard.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Dashboard.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Dashboard.API.dll"]