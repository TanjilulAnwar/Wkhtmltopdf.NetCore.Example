FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
RUN apt-get update -qq && apt-get -y install libgdiplus libc6-dev
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Rotativa", "/src/Rotativa/"]
WORKDIR "/src/Rotativa"
RUN dotnet publish "Rotativa.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
RUN chmod 755 /app/Rotativa/Linux/wkhtmltopdf
ENTRYPOINT ["dotnet", "Rotativa.dll"]