---
title: API Reference
sidebar_position: 1
description: Спецификация Routes API в формате OpenAPI 3.0
---

# API Reference

API для создания, редактирования и просмотра маршрутов.

- **Base URL:** `https://api.routes.app/v1`
- **Версия:** 1.0
- **Формат:** OpenAPI 3.0.2

## Список эндпоинтов

| Метод | Путь | Назначение |
| --- | --- | --- |
| GET | `/user/profile` | Получение профиля пользователя |
| GET | `/routes/my` | Получение маршрутов пользователя |
| POST | `/routes/draft` | Создание черновика маршрута |
| GET | `/routes/{routeId}` | Получение маршрута |
| PATCH | `/routes/{routeId}` | Обновление маршрута |
| POST | `/routes/{routeId}/points` | Добавление точки маршрута |
| DELETE | `/routes/{routeId}/points/{pointId}` | Удаление точки |
| POST | `/routes/{routeId}/publish` | Публикация маршрута |
| GET | `/locations/search?q=` | Поиск локации |
| GET | `/routes/meta` | Получение справочников |

## Полная OpenAPI-спецификация

```yaml
openapi: "3.0.2"
info:
  title: Routes API
  description: API для создания, редактирования и просмотра маршрутов
  version: "1.0"

servers:
  - url: https://api.routes.app/v1

paths:

  /user/profile:
    get:
      summary: Получение профиля пользователя
      responses:
        '200':
          description: Профиль пользователя
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/UserProfile"

  /routes/my:
    get:
      summary: Получение маршрутов пользователя
      responses:
        '200':
          description: Список маршрутов
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/MyRoutesResponse"

  /routes/draft:
    post:
      summary: Создание черновика маршрута
      responses:
        '200':
          description: Черновик создан
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/RouteIdResponse"

  /routes/{routeId}:
    get:
      summary: Получение маршрута
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/RouteId"
      responses:
        '200':
          description: Данные маршрута
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Route"

    patch:
      summary: Обновление маршрута
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/RouteId"
      requestBody:
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/UpdateRouteRequest"
      responses:
        '200':
          description: Успешно обновлено

  /routes/{routeId}/points:
    post:
      summary: Добавление точки
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/RouteId"
      requestBody:
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/CreatePointRequest"
      responses:
        '200':
          description: Точка добавлена

  /routes/{routeId}/points/{pointId}:
    delete:
      summary: Удаление точки
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/RouteId"
        - name: pointId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/PointId"
      responses:
        '200':
          description: Точка удалена

  /routes/{routeId}/publish:
    post:
      summary: Публикация маршрута
      parameters:
        - name: routeId
          in: path
          required: true
          schema:
            $ref: "#/components/schemas/RouteId"
      responses:
        '200':
          description: Маршрут опубликован

  /locations/search:
    get:
      summary: Поиск локации
      parameters:
        - name: q
          in: query
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Результаты поиска
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/LocationSearchResponse"

  /routes/meta:
    get:
      summary: Получение справочников
      responses:
        '200':
          description: Метаданные
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/MetaResponse"


components:
  schemas:

    UserProfile:
      type: object
      properties:
        name:
          type: string
        username:
          type: string
        stats:
          type: object
          properties:
            routes:
              type: integer
            followers:
              type: integer
            following:
              type: integer

    Route:
      type: object
      properties:
        id:
          $ref: "#/components/schemas/RouteId"
        title:
          type: string
        description:
          type: string
        notes:
          type: string
        imageUrl:
          type: string
        status:
          $ref: "#/components/schemas/RouteStatus"
        points:
          type: array
          items:
            $ref: "#/components/schemas/Point"
        itemsToBring:
          type: array
          items:
            type: string
        bestTime:
          type: array
          items:
            $ref: "#/components/schemas/TimeOfDay"

    RouteStatus:
      type: string
      enum: [draft, published]

    Point:
      type: object
      properties:
        id:
          $ref: "#/components/schemas/PointId"
        name:
          type: string
        description:
          type: string
        order:
          type: integer
        location:
          $ref: "#/components/schemas/Location"

    Location:
      type: object
      properties:
        lat:
          type: number
        lng:
          type: number
        address:
          type: string

    UpdateRouteRequest:
      type: object
      properties:
        title:
          type: string
        description:
          type: string
        notes:
          type: string
        imageUrl:
          type: string
        itemsToBring:
          type: array
          items:
            type: string
        bestTime:
          type: array
          items:
            $ref: "#/components/schemas/TimeOfDay"

    CreatePointRequest:
      type: object
      required:
        - name
        - location
      properties:
        name:
          type: string
        description:
          type: string
        location:
          $ref: "#/components/schemas/Location"

    MyRoutesResponse:
      type: object
      properties:
        routes:
          type: array
          items:
            $ref: "#/components/schemas/Route"

    RouteIdResponse:
      type: object
      properties:
        routeId:
          $ref: "#/components/schemas/RouteId"

    LocationSearchResponse:
      type: object
      properties:
        results:
          type: array
          items:
            $ref: "#/components/schemas/Location"

    MetaResponse:
      type: object
      properties:
        itemsToBring:
          type: array
          items:
            type: string
        bestTimeOptions:
          type: array
          items:
            $ref: "#/components/schemas/TimeOfDay"

    TimeOfDay:
      type: string
      enum:
        - morning
        - day
        - evening
        - night

    RouteId:
      type: string
      format: uuid

    PointId:
      type: string
      format: uuid
```
