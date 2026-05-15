# syntax=docker/dockerfile:1 


FROM mcr.microsoft.com/dotnet/sdk:10.0 AS builder 
WORKDIR /app 
COPY backend.csproj ./
RUN dotnet restore
COPY . ./
RUN dotnet publish -c Release -o out 
 
FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app 
COPY --from=builder /app/out .
 
EXPOSE 8080 
CMD ["dotnet", "backend.dll"] 
