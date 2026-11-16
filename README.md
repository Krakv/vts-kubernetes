# VoiceTaskSystem — Kubernetes

Репозиторий содержит Kubernetes-манифесты для развёртывания и управления приложением **[VoiceTaskSystem](https://github.com/Krakv/VoiceTaskSystem)** в Kubernetes-кластере.

Основная задача репозитория — описать инфраструктуру приложения в декларативном виде: какие компоненты должны быть запущены, как они взаимодействуют между собой и какие ресурсы Kubernetes необходимы для их работы.

## Architecture

Приложение состоит из нескольких основных компонентов:

- **Frontend** — пользовательский интерфейс, через который пользователь взаимодействует с системой.
- **Task Manager** — backend-сервис, отвечающий за управление задачами и основную бизнес-логику приложения.
- **Speech Processing** — компонент обработки голосовых данных.
- **Duckling** — сервис для извлечения структурированной информации из естественного языка.
- **PostgreSQL** — база данных для хранения информации приложения.

Компоненты разворачиваются в отдельном Kubernetes namespace `vts`. Для взаимодействия между сервисами используются Kubernetes Services, а конфигурация и чувствительные параметры передаются через ConfigMaps и Secrets.

## Project Structure

```text
├── duckling
├── frontend
├── postgres
│   ├── service.yaml
│   └── statefulset.yaml
├── speech-processing
├── task-manager
│   ├── configmap.yaml
│   ├── deployment.yaml
│   └── service.yaml
├── namespace.yaml
└── README.md
```

## Configuration

Для хранения настроек приложения используются ConfigMaps, а для конфиденциальных данных, например паролей и учётных данных, — Kubernetes Secrets.

Для PostgreSQL настроено постоянное хранилище объёмом 2 GiB, чтобы данные базы сохранялись независимо от жизненного цикла Pod.