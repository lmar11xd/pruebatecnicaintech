FROM mcr.microsoft.com/dotnet/sdk:5.0-focal AS build
WORKDIR /app
EXPOSE 80
EXPOSE 5024
#
# copy csproj and restore as distinct layers
COPY *.sln .
COPY InTech.API/*.csproj ./InTech.API/
COPY InTech.Application/*.csproj ./InTech.Application/
COPY InTech.Core/*.csproj ./InTech.Core/
COPY InTech.Infrastructure/*.csproj ./InTech.Infrastructure/ 
#
RUN dotnet restore 
#
# copy everything else and build app
COPY InTech.API/. ./InTech.API/
COPY InTech.Application/. ./InTech.Application/
COPY InTech.Core/. ./InTech.Core/
COPY InTech.Infrastructure/. ./InTech.Infrastructure/
#
WORKDIR /app/InTech.API
RUN dotnet publish -c Release -o out 
#
FROM mcr.microsoft.com/dotnet/aspnet:5.0-focal AS runtime
WORKDIR /app 
#
COPY --from=build /app/InTech.API/out ./
ENTRYPOINT ["dotnet", "InTech.API.dll"]