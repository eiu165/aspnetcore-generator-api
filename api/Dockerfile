# build stage
FROM microsoft/aspnetcore-build:2 as build-env
WORKDIR /api
COPY api.csproj .  
RUN dotnet restore
COPY . .  
RUN dotnet publish -o /publish

# runtime image stage
FROM microsoft/aspnetcore:2
WORKDIR /publish
COPY --from=build-env /publish . 
ENTRYPOINT ["dotnet", "api.dll"]
