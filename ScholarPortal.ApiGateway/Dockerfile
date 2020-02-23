FROM mcr.microsoft.com/dotnet/core/sdk:3.1-bionic AS build-env
WORKDIR /app

COPY ./src/ScholarPortal.ApiGateway/*.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-bionic
WORKDIR /app

COPY --from=build-env /app/out .
COPY ./src/ScholarPortal.ApiGateway/ntrada.yml ./
COPY ./src/ScholarPortal.ApiGateway/ntrada-async.docker.yml ./

ENV ASPNETCORE_URLS http://*5000
ENV ASPNETCORE_ENVIRONMENT docker

EXPOSE 5000

ENTRYPOINT dotnet ScholarPortal.ApiGateway.dll