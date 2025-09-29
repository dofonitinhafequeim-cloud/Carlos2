-- Script ServerSide (ex: ServerScriptService)
-- Sistema de Roleta de Pets (World 1 ao 21)

local RoletaPets = {}

-- Definir pets de cada world:
local PetsPorWorld = {
    [1] = { {Name = "Pet1", Chance = 50}, {Name = "PetRaro1", Chance = 10}, {Name = "PetLendario1", Chance = 1} },
    [2] = { {Name = "Pet2", Chance = 50}, {Name = "PetRaro2", Chance = 10}, {Name = "PetLendario2", Chance = 1} },
    -- ...
    [21] = { {Name = "Pet21", Chance = 50}, {Name = "PetRaro21", Chance = 10}, {Name = "PetLendario21", Chance = 1} },
}

-- Função para sortear pet baseado nas chances
local function SortearPet(world)
	if not PetsPorWorld[world] then return nil end
	local lista = PetsPorWorld[world]

	-- soma total das chances
	local totalChance = 0
	for _, pet in ipairs(lista) do
		totalChance = totalChance + pet.Chance
	end

	-- sorteio
	local sorteio = math.random() * totalChance
	local acumulado = 0
	for _, pet in ipairs(lista) do
		acumulado = acumulado + pet.Chance
		if sorteio <= acumulado then
			return pet.Name
		end
	end
	return nil
end

-- Exemplo: Função pública para jogadores
function RoletaPets.Girar(player, world)
	local pet = SortearPet(world)
	if pet then
		print(player.Name .. " ganhou o pet: " .. pet)
		-- Aqui você pode dar o pet de verdade ao player:
		-- (ex: clonar um modelo de pet e colocar no inventário do player)
	else
		warn("World inválido ou sem pets configurados.")
	end
end

return RoletaPets
