# build stage
FROM microsoft/aspnetcore-build as build-env
WORKDIR /api
COPY api.csproj .  
RUN dotnet restore
COPY . .  
RUN dotnet publish -o /publish

# runtime image stage
FROM microsoft/aspnetcore
WORKDIR /publish
COPY --from=build-env /publish . 
ENTRYPOINT ["dotnet", "/api.dll"]
