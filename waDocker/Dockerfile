FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["waDocker/waDocker.csproj", "waDocker/"]
RUN dotnet restore "waDocker/waDocker.csproj"
COPY . .
WORKDIR "/src/waDocker"
RUN dotnet build "waDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "waDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "waDocker.dll"]