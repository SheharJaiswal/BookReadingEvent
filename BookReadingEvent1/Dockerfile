#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BookReadingEvent1/BookReadingEvent1.csproj", "BookReadingEvent1/"]
COPY ["Business_Logic_Layer/Business_Logic_Layer.csproj", "Business_Logic_Layer/"]
COPY ["Data_Acess_Layer/Data_Acess_Layer.csproj", "Data_Acess_Layer/"]
RUN dotnet restore "BookReadingEvent1/BookReadingEvent1.csproj"
COPY . .
WORKDIR "/src/BookReadingEvent1"
RUN dotnet build "BookReadingEvent1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BookReadingEvent1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BookReadingEvent1.dll"]