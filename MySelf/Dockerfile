FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MySelf/MySelf.csproj", "MySelf/"]
RUN dotnet restore "MySelf/MySelf.csproj"
COPY . .
WORKDIR "/src/MySelf"
RUN dotnet build "MySelf.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MySelf.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MySelf.dll"]
