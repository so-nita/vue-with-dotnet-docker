#VueApp.Server/Dockerfile

# Stage 1: Build the .NET application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
# Copy the server project file and restore dependencies
COPY VueApp.Server.csproj ./
RUN dotnet restore VueApp.Server.csproj
# Copy the entire solution and build
COPY . .
WORKDIR /src
RUN dotnet build "VueApp.Server.csproj" -c Release -o /app/build

# Stage 2: Publish the .NET application
FROM build AS publish
WORKDIR /src
RUN dotnet publish "VueApp.Server.csproj" -c Release -o /app/publish

# Stage 3: Create the final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
EXPOSE 8180 
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VueApp.Server.dll"]