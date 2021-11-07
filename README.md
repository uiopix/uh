player.onItemInteracted(SEEDS, function () {
    agent.teleportToPlayer()
    for (let index = 0; index < 111; index++) {
        for (let index = 0; index < 4; index++) {
            for (let index = 0; index < 3; index++) {
                agent.move(FORWARD, 1)
                agent.destroy(DOWN)
                agent.collectAll()
                agent.destroy(RIGHT)
                agent.destroy(FORWARD)
            }
            agent.turn(RIGHT_TURN)
        }
        agent.move(DOWN, 1)
    }
})
player.onItemInteracted(STONE_AXE, function () {
    agent.teleportToPlayer()
    for (let index = 0; index < 5; index++) {
        agent.move(FORWARD, 1)
        agent.destroy(UP)
        agent.destroy(DOWN)
        agent.destroy(RIGHT)
        agent.destroy(LEFT)
        agent.destroy(FORWARD)
    }
})
function Mine2 () {
    row_width = 0
    agent.teleport(mineZYX, SOUTH)
    for (let index = 0; index < Math.round((mineZYX.getValue(Axis.Y) - 11) / 2); index++) {
        agent.destroy(FORWARD)
        agent.move(FORWARD, 1)
        agent.destroy(UP)
        agent.collectAll()
        agent.destroy(DOWN)
        agent.move(DOWN, 1)
        if (agent.inspect(AgentInspection.Block, DOWN) == AIR) {
            agent.setSlot(2)
            agent.place(DOWN)
        }
        agent.collectAll()
    }
    agent.turn(RIGHT_TURN)
    for (let index = 0; index < 2; index++) {
        agent.destroy(FORWARD)
        agent.move(FORWARD, 1)
        agent.destroy(UP)
        agent.collectAll()
    }
    agent.turn(RIGHT_TURN)
    for (let index = 0; index < Math.round((mineZYX.getValue(Axis.Y) - 11) / 2); index++) {
        agent.destroy(FORWARD)
        agent.move(FORWARD, 1)
        agent.destroy(UP)
        agent.collectAll()
        agent.destroy(DOWN)
        agent.move(DOWN, 1)
        if (agent.inspect(AgentInspection.Block, DOWN) == AIR) {
            agent.setSlot(2)
            agent.place(DOWN)
        }
        agent.collectAll()
    }
    agent.move(FORWARD, rounds * 15)
    for (let index = 0; index < 5 + rounds * 5; index++) {
        agent.turn(LEFT_TURN)
        row_width = 0
        while (row_width < setLength) {
            agent.destroy(FORWARD)
            agent.move(FORWARD, 1)
            agent.destroy(UP)
            agent.collectAll()
            Scan_and_collect2()
            row_width += 1
        }
        agent.turn(LEFT_TURN)
        agent.turn(LEFT_TURN)
        row_width = 0
        agent.move(FORWARD, setLength)
        while (row_width < setLength) {
            agent.destroy(FORWARD)
            agent.move(FORWARD, 1)
            agent.destroy(UP)
            agent.collectAll()
            Scan_and_collect2()
            row_width += 1
        }
        rows += 1
        agent.turn(LEFT_TURN)
        agent.turn(LEFT_TURN)
        row_width = 0
        agent.move(FORWARD, setLength)
        agent.turn(RIGHT_TURN)
        for (let index = 0; index < 3; index++) {
            agent.destroy(FORWARD)
            agent.move(FORWARD, 1)
            agent.destroy(UP)
            Scan_and_collect2()
            agent.collectAll()
        }
    }
}
player.onItemInteracted(WHEAT, function () {
    agent.turn(LEFT_TURN)
})
player.onChat("rowlength", function (num1) {
    setLength = num1
    player.say("Set length of mines to " + num1)
})
function Scan_and_collect2 () {
    if (agent.inspect(AgentInspection.Block, UP) == IRON_ORE) {
        agent.destroy(UP)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, DOWN) == IRON_ORE) {
        agent.destroy(DOWN)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, LEFT) == IRON_ORE) {
        agent.destroy(LEFT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, RIGHT) == IRON_ORE) {
        agent.destroy(RIGHT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, UP) == COAL_ORE) {
        agent.destroy(UP)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, DOWN) == COAL_ORE) {
        agent.destroy(DOWN)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, LEFT) == COAL_ORE) {
        agent.destroy(LEFT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, RIGHT) == COAL_ORE) {
        agent.destroy(RIGHT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, UP) == REDSTONE_ORE) {
        agent.destroy(UP)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, DOWN) == REDSTONE_ORE) {
        agent.destroy(DOWN)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, LEFT) == REDSTONE_ORE) {
        agent.destroy(LEFT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, RIGHT) == REDSTONE_ORE) {
        agent.destroy(RIGHT)
        agent.collectAll()
    }
    if (agent.inspect(AgentInspection.Block, UP) == DIAMOND_ORE) {
        agent.destroy(UP)
        agent.move(UP, 1)
        ways.push(1)
        agent.collectAll()
        Scan_and_collect2()
    }
    if (agent.inspect(AgentInspection.Block, DOWN) == DIAMOND_ORE) {
        agent.destroy(DOWN)
        agent.move(DOWN, 1)
        ways.push(2)
        agent.collectAll()
        Scan_and_collect2()
    }
    if (agent.inspect(AgentInspection.Block, LEFT) == DIAMOND_ORE) {
        agent.destroy(LEFT)
        agent.move(LEFT, 1)
        ways.push(3)
        agent.collectAll()
        Scan_and_collect2()
    }
    if (agent.inspect(AgentInspection.Block, RIGHT) == DIAMOND_ORE) {
        agent.destroy(RIGHT)
        agent.move(RIGHT, 1)
        ways.push(4)
        agent.collectAll()
        Scan_and_collect2()
    }
    if (agent.inspect(AgentInspection.Block, FORWARD) == DIAMOND_ORE) {
        agent.destroy(FORWARD)
        agent.move(FORWARD, 1)
        ways.push(5)
        agent.collectAll()
        Scan_and_collect2()
    }
    if (agent.inspect(AgentInspection.Block, BACK) == DIAMOND_ORE) {
        agent.destroy(BACK)
        agent.move(BACK, 1)
        ways.push(6)
        agent.collectAll()
        Scan_and_collect2()
    }
    ways.reverse()
    for (let index82 = 0; index82 <= ways.length; index82++) {
        if (ways[index82] == 1) {
            agent.move(DOWN, 1)
        } else if (ways[index82] == 2) {
            agent.move(UP, 1)
        } else if (ways[index82] == 3) {
            agent.move(RIGHT, 1)
        } else if (ways[index82] == 4) {
            agent.move(LEFT, 1)
        } else if (ways[index82] == 5) {
            agent.move(BACK, 1)
        } else if (ways[index82] == 6) {
            agent.move(FORWARD, 1)
        }
    }
    ways = []
}
player.onItemInteracted(TRIDENT, function () {
    blocks.fill(
    SAND,
    player.position(),
    pos(-4, -19, -4),
    FillOperation.Hollow
    )
})
player.onItemInteracted(COAL, function () {
    agent.teleportToPlayer()
})
player.onItemInteracted(APPLE, function () {
    player.teleport(pos(randint(-100, 100), 1, randint(-100, 100)))
})
player.onItemInteracted(IRON_SHOVEL, function () {
	
})
player.onItemInteracted(GUNPOWDER, function () {
    agent.teleportToPlayer()
    for (let index = 0; index < 43; index++) {
        agent.move(FORWARD, 1)
        agent.place(RIGHT)
        agent.place(LEFT)
        agent.place(DOWN)
    }
})
player.onChat("mine", function () {
	
})
player.onItemInteracted(WOODEN_PICKAXE, function () {
    agent.teleportToPlayer()
    mineZYX = agent.getPosition()
    while (true) {
        Mine2()
        agent.teleportToPlayer()
        agent.dropAll(UP)
        rounds += 1
        loops.pause(5000)
    }
})
let ways: number[] = []
let rounds = 0
let mineZYX: Position = null
let row_width = 0
let setLength = 0
let rows = 1
setLength = 10
agent.dropAll(UP)
