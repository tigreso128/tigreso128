- 👋 hola, yo soy @tigreso128
- casi el mejor de bloxd.io
- https://bloxd.io
- // ==UserScript==
// @name        ...
// @namespace    http://tampermonkey.net/
// @version      2024-09-09
// @description  try to take over the world!
// @author       You
// @match        http://bloxd.io/
// @icon         data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==
// @grant        GM_addStyle
// ==/UserScript==
// @downloadURL https://update.greasyfork.org/scripts/487836/miniblox%kill aura%20counter.user.js
// @updateURL https://update.greasyfork.org/scripts/487836/miniblox%kill aura%20counter.meta.js

(function() {
    'use script';

    -- Variables
local player = game.Players.LocalPlayer
local humanoidRootPart = player.Character:WaitForChild("HumanoidRootPart")
local attackRadius = 40 -- Radio de ataque en studs
local damageAmount = 10 -- Cantidad de daño que aplicará el ataque
local attackCooldown = 2 -- Tiempo de espera entre ataques (en segundos)

-- Función para atacar a todos los seres vivos cercanos
local function attackNearbyEnemies()
    for _, object in pairs(workspace:GetChildren()) do
        if object:FindFirstChild("Humanoid") and object ~= player.Character then
            local humanoid = object:FindFirstChild("Humanoid")
            local enemyRootPart = object:FindFirstChild("HumanoidRootPart")

            if humanoid and enemyRootPart then
                local distance = (humanoidRootPart.Position - enemyRootPart.Position).Magnitude

                if distance <= attackRadius then
                    humanoid:TakeDamage(damageAmount)
                    print("Atacado:", object.Name)
                end
            end
        end
    end
end

-- Ciclo para atacar cada cierto tiempo
while true do
    attackNearbyEnemies()
    wait(attackCooldown)
end

})();
