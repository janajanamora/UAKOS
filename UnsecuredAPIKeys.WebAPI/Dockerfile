# ---------- 用 SDK 镜像编译 ----------
FROM mcr.microsoft.com/dotnet/sdk:9.0-preview AS build
WORKDIR /src
COPY . .

# 在仓库根执行：一次还原所有项目
RUN dotnet restore ./UnsecuredAPIKeys.sln

# 发布指定 WebAPI 项目，连依赖一起编进 /app
RUN dotnet publish ./UnsecuredAPIKeys.WebAPI.csproj -c Release -o /app

# ---------- 用运行时镜像启动 ----------
FROM mcr.microsoft.com/dotnet/aspnet:9.0-preview
WORKDIR /app
COPY --from=build /app .

ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}
EXPOSE 10000
ENTRYPOINT ["dotnet", "UnsecuredAPIKeys.WebAPI.dll"]
