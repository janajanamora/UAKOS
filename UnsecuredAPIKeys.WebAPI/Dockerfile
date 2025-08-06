# ---------- 用 SDK 镜像编译 ----------
FROM mcr.microsoft.com/dotnet/sdk:9.0-preview AS build
WORKDIR /src
COPY . .

# ❶ 还原 WebAPI 项目（解决方案文件被忽略了）
RUN dotnet restore ./UnsecuredAPIKeys.WebAPI.csproj

# ❷ 发布同一个项目，连依赖一起进 /app
RUN dotnet publish ./UnsecuredAPIKeys.WebAPI.csproj -c Release -o /app

# ---------- 用运行时镜像启动 ----------
FROM mcr.microsoft.com/dotnet/aspnet:9.0-preview
WORKDIR /app
COPY --from=build /app .

ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}
EXPOSE 10000
ENTRYPOINT ["dotnet", "UnsecuredAPIKeys.WebAPI.dll"]
