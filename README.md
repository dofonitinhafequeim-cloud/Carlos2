-- RoletaPets.lua
-- Sistema de roleta de pets (World 1 ao 21)

local RoletaPets = {}

-- Tabela com pets por world e chances
local PetsPorWorld = {
    [1] = {
        {Name = "Pet1", Chance = 50},
        {Name = "PetRaro1", Chance = 10},
        {Name = "PetLendario1", Chance = 1}
    },
    [2] = {
        {Name = "Pet2", Chance = 50},
        {Name = "PetRaro2", Chance = 10},
        {Name = "PetLendario2", Chance = 1}
    },
    -- Adicione os worlds até 21:
    [21] = {
        {Name = "Pet21", Chance = 50},
        {Name = "PetRaro21", Chance = 10},
        {Name = "PetLendario21", Chance = 1}
    },
}

-- Função interna para sortear pet
local function SortearPet(world)
	if not PetsPorWorld[world] then
		return nil
	end

	local lista = PetsPorWorld[world]
	local totalChance = 0
	for _, pet in ipairs(lista) do
		totalChance += pet.Chance
	end

	local sorteio = math.random() * totalChance
	local acumulado = 0
	for _, pet in ipairs(lista) do
		acumulado += pet.Chance
		if sorteio <= acumulado then
			return pet.Name
		end
	end

	return nil
end

-- Função pública para girar roleta
function RoletaPets.Girar(player, world)
	local pet = SortearPet(world)
	if pet then
		print(player.Name .. " ganhou o pet: " .. pet)
		-- Aqui você pode colocar o código para dar o pet ao player
	else
		warn("World inválido ou sem pets configurados.")
	end
end

return RoletaPets
