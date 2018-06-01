FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base  #�������ǽ�ʹ���ĸ������������������ǵ�������
WORKDIR /app  #����Ŀ¼����Ϊ'/ app'��������ǵ�dockerfile�е����������������ִ��
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
WORKDIR /src
COPY DockerCore/DockerCore.csproj DockerCore/  #���ǽ�.csproj�ļ����Ƶ���ʱ������'/ app'Ŀ¼�С���������������Ϊ.csproj�ļ�������������Ŀ��Ҫ�������������б�
RUN dotnet restore DockerCore/DockerCore.csproj

COPY . .
WORKDIR /src/DockerCore
RUN dotnet build DockerCore.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerCore.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerCore.dll"]