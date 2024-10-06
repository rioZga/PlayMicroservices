FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

ENV DOTNET_URLS=http://+:5000

COPY ["./Play.Catalog.Services/Play.Catalog.Services.csproj", "./"]
COPY ./packages ./packages
COPY ./Play.Catalog.Services/NuGet.config ./

RUN dotnet restore "./Play.Catalog.Services.csproj" --configfile ./NuGet.config

COPY ./Play.Catalog.Services/. .

WORKDIR "/src/"

RUN dotnet build "./Play.Catalog.Services.csproj" -c Release -o /app/build

FROM build AS runtime
WORKDIR /app
COPY --from=build /app/build ./

ENTRYPOINT ["dotnet", "Play.Catalog.Services.dll"]