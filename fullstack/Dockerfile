# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy everything
COPY . ./

# Restore dependencies
RUN dotnet restore fullstack.sln

# Publish the project
RUN dotnet publish fullstack/fullstack.csproj -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Expose port for external access (optional but good for clarity)
EXPOSE 8080

# Copy published app from build stage
COPY --from=build /app/publish .

# Set entry point
ENTRYPOINT ["dotnet", "fullstack.dll"]

