# Тестовая сцена для MVP

Огороженный завод. В середине сдание с цехами и вокруг двор. Во дворе разные бочки  и прочее, пара вагонов и машин. Разбросано оружие (труба, пистолет, автомат) и ресурсы (камни ,палки, металолом). Внутри цеха есть верстак. На верстаке можно крафтить патроны и оружие (из палок и камней) и чинить оружие. Внутри 1 НПС. Снаружи спавнятся враги.  

# MVP "Завод" — Техническое задание вертикального среза

## 1. Цель MVP
Проверить "фан" (fun core loop): Ощущение прогрессии от беспомощного беглеца до вооруженного бойца в динамически меняющемся мире.

## 2. Игровая локация: Огороженный завод
*   Двор (Зона риска): Открытое пространство с укрытиями (вагоны, машины). Место спавна врагов и ресурсов.
*   Цех (Безопасная зона): Здание в центре. Содержит Верстак и 1 НПС. Враги не заходят внутрь.
*   Hazard-точки: Группы бочек и луж во дворе, которые активируются при росте Энтропии.

## 3. Геймплейный цикл (The Loop)
*   Spawn: Игрок появляется в углу двора без оружия.
*   Scavenge: Поиск Трубы (первое оружие) за укрытием. Сбор палок и камней во дворе.
*   Combat: Столкновение с врагами. Использование бочек (взрывы, ток) для контроля толпы.
*   Craft: Прорыв в Цех к Верстаку. Превращение ресурсов в Пистолет.
*   Entropy: Убийство Босса -> Рост Энтропии -> Окружение двора мутирует (лужи горят).

## 4. Техническая структура (Node Tree)

### Игрок (CharacterBody3D)
*   StatsComponent: Хранит HP и обрабатывает смерть.
*   Inventory: Список ресурсов (палки, камни) и текущее активное оружие.
*   MovementController: Логика бега и замедления при попадании в зону ELEC.

### Окружение (StaticBody3D / Area3D)
*   Слой 1 (World): Стены, пол, вагоны.
*   Слой 4 (Interactables): Подбираемые предметы (Палка, Камень, Труба).
*   Слой 5 (Hazards): Бочки с HP. При разрушении включают зону урона (Area3D).

### Системы (Autoload / Global)
*   EntropyManager: Хранит уровень хаоса. Сигналит объектам о смене состояния.
*   EnemySpawner: Создает врагов во дворе, чья сила зависит от Энтропии.
*   Workbench (Area3D): Находится в цеху. Рецепт: 2 палки + 2 камня = Пистолет.

## 5. Параметры ресурсов и Крафта
*   Труба: Оружие ближнего боя. Находится за вагоном. Позволяет отбиваться.
*   Палка / Камень: Базовые ресурсы. Разбросаны во дворе. Нужны для крафта.
*   Пистолет: Оружие дальнего боя. Создается на Верстаке из палок и камней.
*   Бочка (ELEC): Объект окружения. При взрыве замедляет всех вокруг на 5 секунд.

## 6. Критерии проверки Веселости
*   Ритм: Не слишком ли долго бегать за ресурсами?
*   Опасность: Ощущается ли адреналин в начале игры без оружия?
*   Удовлетворение: Насколько круто ощущается прогрессия от палки до пистолета?
*   Динамика: Заставляет ли Энтропия менять маршруты передвижения по двору?


# Промпты
Двор завода (Экстерьер)
Этот промпт создаст общую атмосферу: забор, вагоны и брошенные авто.
Isometric POV, pixel art, 16-bit, Fallout 1 style, industrial factory yard with rusted chain-link fence, two derelict train wagons, and skeleton of a 1950s car, scattered oil drums, cracked concrete, harsh midday sun with high contrast shadows, dusty ochre and rusted iron, sharp pixels, low fidelity, nostalgic and detailed atmosphere --width 512 --height 256

Панорама завода (Жаркая пустыня Орегона) (закат)
Wide-angle side view, pixel art, 16-bit, Fallout 1 style, massive sun-bleached concrete factory complex under a hazy burning sky, swaying dry tumbleweeds, heat haze ripples, distant reddish plateaus, intense golden hour sun, warm terracotta and scorched yellow, sharp pixels, low fidelity, nostalgic and detailed atmosphere --width 512 --height 256

Завод при дневном освещении (High Desert)
Wide-angle side view, pixel art, 16-bit, Fallout 1 style, concrete factory building with sharp outlines under a clear vast sky, dry yellow shrubs, scattered industrial debris, harsh direct vertical sunlight with pitch-black shadows, desiccated tan, concrete grey and pale blue, sharp pixels, low fidelity, nostalgic and detailed atmosphere --width 512 --height 256

Грузовой вагон (Industrial Red)
Side view, pixel art, 16-bit, Fallout 1 style, heavy industrial boxcar with corrugated metal sides and a sliding heavy door, chipped deep oxide red paint, rusted steel wheels, weathered white stenciled serial numbers, harsh direct sunlight, dark crimson and burnt sienna, sharp pixels, low fidelity, nostalgic and detailed atmosphere --width 512 --height 256

Человекообразный робот (Retro-Humanoid Bot)
Frontal view, pixel art, 16-bit, Fallout 1 style, clunky humanoid robot with a cylindrical head and glowing yellow visor, bulky metal torso with visible rivets and chest gauges, hydraulic piston joints in arms and legs, harsh direct sunlight reflecting off scratched metal, dull silver chrome and tarnished brass, sharp pixels, low fidelity, nostalgic and detailed atmosphere --width 512 --height 256
