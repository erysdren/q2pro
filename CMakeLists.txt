cmake_minimum_required(VERSION 3.5)

project(q2pro LANGUAGES C)

include(FindPkgConfig)
pkg_search_module(SDL2 REQUIRED sdl2)

set(Q2PRO_COMMON_SRC
	"src/common/bsp.c"
	"src/common/cmd.c"
	"src/common/cmodel.c"
	"src/common/common.c"
	"src/common/crc.c"
	"src/common/cvar.c"
	"src/common/error.c"
	"src/common/field.c"
	"src/common/fifo.c"
	"src/common/files.c"
	"src/common/hash_map.c"
	"src/common/math.c"
	"src/common/mdfour.c"
	"src/common/msg.c"
	"src/common/net/chan.c"
	"src/common/net/net.c"
	"src/common/pmove/common.c"
	"src/common/pmove/new.c"
	"src/common/pmove/old.c"
	"src/common/prompt.c"
	"src/common/sizebuf.c"
	"src/common/utils.c"
	"src/common/zone.c"
	"src/shared/shared.c"
)

set(Q2PRO_CLIENT_SRC
	"src/client/ascii.c"
	"src/client/console.c"
	"src/client/demo.c"
	"src/client/download.c"
	"src/client/effects.c"
	"src/client/entities.c"
	"src/client/input.c"
	"src/client/keys.c"
	"src/client/locs.c"
	"src/client/main.c"
	"src/client/newfx.c"
	"src/client/parse.c"
	"src/client/precache.c"
	"src/client/predict.c"
	"src/client/refresh.c"
	"src/client/screen.c"
	"src/client/sound/main.c"
	"src/client/sound/mem.c"
	"src/client/tent.c"
	"src/client/view.c"
	"src/common/async.c"
	"src/server/commands.c"
	"src/server/entities.c"
	"src/server/game.c"
	"src/server/init.c"
	"src/server/main.c"
	"src/server/send.c"
	"src/server/user.c"
	"src/server/world.c"
	"src/shared/m_flash.c"
)

set(Q2PRO_UI_SRC
	"src/client/ui/demos.c"
	"src/client/ui/menu.c"
	"src/client/ui/playerconfig.c"
	"src/client/ui/playermodels.c"
	"src/client/ui/script.c"
	"src/client/ui/servers.c"
	"src/client/ui/ui.c"
)

set(Q2PRO_REFRESH_SRC
	"src/refresh/draw.c"
	"src/refresh/hq2x.c"
	"src/refresh/images.c"
	"src/refresh/legacy.c"
	"src/refresh/main.c"
	"src/refresh/mesh.c"
	"src/refresh/models.c"
	"src/refresh/qgl.c"
	"src/refresh/shader.c"
	"src/refresh/sky.c"
	"src/refresh/state.c"
	"src/refresh/surf.c"
	"src/refresh/tess.c"
	"src/refresh/texture.c"
	"src/refresh/world.c"
)

set(Q2PRO_SERVER_SRC
	"src/client/null.c"
	"src/server/commands.c"
	"src/server/entities.c"
	"src/server/game.c"
	"src/server/init.c"
	"src/server/main.c"
	"src/server/send.c"
	"src/server/user.c"
	"src/server/world.c"
)

set(Q2PRO_GAME_SRC
	"src/game/g_ai.c"
	"src/game/g_chase.c"
	"src/game/g_cmds.c"
	"src/game/g_combat.c"
	"src/game/g_func.c"
	"src/game/g_items.c"
	"src/game/g_main.c"
	"src/game/g_misc.c"
	"src/game/g_monster.c"
	"src/game/g_phys.c"
	"src/game/g_ptrs.c"
	"src/game/g_save.c"
	"src/game/g_spawn.c"
	"src/game/g_svcmds.c"
	"src/game/g_target.c"
	"src/game/g_trigger.c"
	"src/game/g_turret.c"
	"src/game/g_utils.c"
	"src/game/g_weapon.c"
	"src/game/m_actor.c"
	"src/game/m_berserk.c"
	"src/game/m_boss2.c"
	"src/game/m_boss31.c"
	"src/game/m_boss32.c"
	"src/game/m_boss3.c"
	"src/game/m_brain.c"
	"src/game/m_chick.c"
	"src/game/m_flipper.c"
	"src/game/m_float.c"
	"src/game/m_flyer.c"
	"src/game/m_gladiator.c"
	"src/game/m_gunner.c"
	"src/game/m_hover.c"
	"src/game/m_infantry.c"
	"src/game/m_insane.c"
	"src/game/m_medic.c"
	"src/game/m_move.c"
	"src/game/m_mutant.c"
	"src/game/m_parasite.c"
	"src/game/m_soldier.c"
	"src/game/m_supertank.c"
	"src/game/m_tank.c"
	"src/game/p_client.c"
	"src/game/p_hud.c"
	"src/game/p_trail.c"
	"src/game/p_view.c"
	"src/game/p_weapon.c"
	"src/shared/m_flash.c"
	"src/shared/shared.c"
)

add_executable(q2pro ${Q2PRO_COMMON_SRC} ${Q2PRO_CLIENT_SRC} ${Q2PRO_REFRESH_SRC})

target_include_directories(q2pro PRIVATE inc ${SDL2_INCLUDE_DIRS})
target_link_libraries(q2pro PRIVATE ${SDL2_LIBRARIES})
target_compile_definitions(q2pro PRIVATE
	USE_CLIENT=1
	USE_REF=1
	USE_LITTLE_ENDIAN
	VERSION=$<QUOTE>PSP$<QUOTE>
	BUILDSTRING=$<QUOTE>SORRYNO$<QUOTE>
	CPUSTRING=$<QUOTE>${CMAKE_SYSTEM_PROCESSOR}$<QUOTE>
	BASEGAME=$<QUOTE>baseq2$<QUOTE>
	DEFGAME=$<QUOTE>baseq2$<QUOTE>
)

if(PSP)
	create_pbp_file(
		TARGET ${PROJECT_NAME}
		ICON_PATH NULL
		BACKGROUND_PATH NULL
		PREVIEW_PATH NULL
		TITLE ${PROJECT_NAME}
	)
endif()
