FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 24144
EXPOSE 44392

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY . .
RUN dotnet build "DatingApp.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DatingApp.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
EXPOSE 5000
ENTRYPOINT ["dotnet", "DatingApp.API.dll"]