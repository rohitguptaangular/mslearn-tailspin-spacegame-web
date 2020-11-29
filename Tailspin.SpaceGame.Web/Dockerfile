FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY Tailspin.SpaceGame.Web/*.csproj ./Tailspin.SpaceGame.Web/
RUN dotnet restore

# copy everything else and build app
COPY Tailspin.SpaceGame.Web/. ./Tailspin.SpaceGame.Web/
WORKDIR /app/Tailspin.SpaceGame.Web
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS runtime
WORKDIR /app
COPY --from=build /app/Tailspin.SpaceGame.Web/out ./
ENTRYPOINT ["dotnet", "aspnetapp.dll"]