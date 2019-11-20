FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["DC.CP.Web.csproj", "DC.CP.Web/"]
RUN dotnet restore "DC.CP.Web/DC.CP.Web.csproj"
COPY . .
WORKDIR "/src/DC.CP.Web"
RUN dotnet build "DC.CP.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DC.CP.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DC.CP.Web.dll"]
