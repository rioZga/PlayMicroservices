FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

ENV DOTNET_URLS=http://+:5001

COPY ["./Play.Inventory/Play.Inventory.Service.csproj", "./"]
COPY ./packages ./packages
COPY ./Play.Inventory/NuGet.config ./

RUN dotnet restore "./Play.Inventory.Service.csproj" --configfile ./NuGet.config

COPY ./Play.Inventory/. .

WORKDIR "/src/"

RUN dotnet build "./Play.Inventory.Service.csproj" -c Release -o /app/build

FROM build AS runtime
WORKDIR /app
COPY --from=build /app/build ./

ENTRYPOINT ["dotnet", "Play.Inventory.Service.dll"]