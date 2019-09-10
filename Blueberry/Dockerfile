FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Blueberry/Blueberry.csproj", "Blueberry/"]
RUN dotnet restore "Blueberry/Blueberry.csproj"
COPY . .
WORKDIR "/src/Blueberry"
RUN dotnet build "Blueberry.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Blueberry.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Blueberry.dll"]