# 
# Copyright 2016 - 2017 Nesterov A.
# 
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
# 
# http ://www.apache.org/licenses/LICENSE-2.0
# 
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

include_directories(
	.
	./hl2
	./episodic

	../shared
	../shared/hl2
	../shared/episodic
	../shared/econ
	
	../../public
	../../common
	../../public
	../../public/tier0
	../../public/tier1
)

link_directories(
	../../lib/public
)

if(MSVC)
	# D'oh! Wtf, Valve?
	set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} /SAFESEH:NO /NODEFAULTLIB:libc /NODEFAULTLIB:libcd")
	set(CMAKE_SHARED_LINKER_FLAGS_DEBUG "${CMAKE_SHARED_LINKER_FLAGS_DEBUG} /NODEFAULTLIB:libcmt")
	set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "${CMAKE_SHARED_LINKER_FLAGS_RELEASE} /NODEFAULTLIB:libcmtd /OPT:ICF /OPT:REF")
	set(CMAKE_SHARED_LINKER_FLAGS_RELWITHDEBINFO "${CMAKE_SHARED_LINKER_FLAGS_RELWITHDEBINFO} /NODEFAULTLIB:libcmtd /OPT:ICF /OPT:REF")
endif()

add_definitions(
	-D_HAS_ITERATOR_DEBUGGING=0
	-DRAD_TELEMETRY_DISABLED
	-DCOMPILER_MSVC32
	# -DBINK_VIDEO
	# -DAVI_VIDEO
	# -DWMV_VIDEO
	-DGAME_DLL
	-DVECTOR
	-DVERSION_SAFE_STEAM_API_INTERFACES
	-DPROTECTED_THINGS_ENABLE
	-DHL2_DLL
	-DHL2_EPISODIC
	-DUSES_SAVERESTORE
)

if(WIN32)
	add_definitions(
		-DWIN32
		-D_WIN32
		-D_USRDLL
		-D_ITERATOR_DEBUG_LEVEL=0
	)
endif()

# Blamod variables framework
set(BLAMOD_FW_FILES
	../blamod/blamodvar.cpp
	../blamod/blamodvar.h

	../blamod/blamod_gamerules.cpp

	../blamod/ent_blamod_timer.cpp

	../blamod/blamod_triggerdelay.cpp
)
source_group(Blamod FILES ${BLAMOD_FW_FILES})

add_library(server SHARED
	../../public/mathlib/amd3dx.h
	../shared/ammodef.h
	base_transmit_proxy.h
	../../public/basehandle.h
	basetempentity.h
	../../public/tier0/basetypes.h
	../shared/beam_flags.h
	../../public/tier1/bitbuf.h
	../../public/bitvec.h
	../../public/bone_accessor.h
	../../public/bspfile.h
	../../public/bspflags.h
	../../public/mathlib/bumpvects.h
	../../public/tier1/characterset.h
	../../public/tier1/checksum_md5.h
	../../public/client_class.h
	../../public/client_textmessage.h
	../../public/cmodel.h
	../../public/vphysics/collision_set.h
	../../public/Color.h
	../../public/tier0/commonmacros.h
	../../public/mathlib/compressed_light_cube.h
	../../public/mathlib/compressed_vector.h
	../../public/const.h
	../../public/vphysics/constraints.h
	../../public/coordsize.h
	bla/timer.h
	cplane.h
	damagemodifier.h
	../../public/datamap.h
	../../public/tier0/dbg.h
	../shared/death_pose.h
	../shared/decals.h
	../../public/dlight.h
	../../public/dt_common.h
	../../public/dt_recv.h
	../../public/dt_send.h
	../../public/dt_utlvector_common.h
	../../public/dt_utlvector_send.h
	../shared/effect_dispatch_data.h
	../shared/ehandle.h
	../shared/entitydatainstantiator.h
	../shared/entitylist_base.h
	../shared/env_detail_controller.h
	EventLog.h
	../shared/expressionsample.h
	../../public/tier0/fasttimer.h
	../../public/filesystem.h
	../../public/filesystem_helpers.h
	../../public/tier1/fmtstr.h
	fogcontroller.h
	../../public/vphysics/friction.h
	../shared/func_ladder.h
	../shared/gameeventdefs.h
	../shared/GameEventListener.h
	../shared/gamerules_register.h
	../../public/gametrace.h
	globals.h
	../../public/globalvars_base.h
	../shared/groundlink.h
	../../public/haptics/haptic_utils.h
	../shared/hl2/hl2_vehicle_radar.h
	../../public/iachievementmgr.h
	../../public/appframework/IAppSystem.h
	../../public/icliententity.h
	../../public/iclientnetworkable.h
	../../public/iclientrenderable.h
	../../public/iclientunknown.h
	../../public/engine/ICollideable.h
	../../public/tier0/icommandline.h
	../../public/icvar.h
	../shared/IEffects.h
	../../public/engine/IEngineSound.h
	../../public/engine/IEngineTrace.h
	../../public/igameevents.h
	../shared/igamemovement.h
	../../public/ihandleentity.h
	../shared/econ/ihasowner.h
	../../public/ihltv.h
	../../public/ihltvdirector.h
	../../public/vstdlib/IKeyValuesSystem.h
	hl2/prop_gravity_ball.h
	ilagcompensationmanager.h
	../../public/vgui/ILocalize.h
	../../public/materialsystem/imaterial.h
	../../public/materialsystem/imaterialsystem.h
	../../public/materialsystem/imaterialvar.h
	../shared/imovehelper.h
	../shared/in_buttons.h
	../../public/inetchannelinfo.h
	../shared/iplayeranimstate.h
	../shared/ipredictionsystem.h
	../../public/irecipientfilter.h
	../../public/isaverestore.h
	../../public/iscratchpad3d.h
	../../public/iserverentity.h
	../../public/iservernetworkable.h
	../../public/iserverunknown.h
	../../public/SoundEmitterSystem/isoundemittersystembase.h
	../../public/ispatialpartition.h
	../../public/engine/IStaticPropMgr.h
	../shared/itempents.h
	../../public/engine/ivdebugoverlay.h
	../shared/IVehicle.h
	../../public/engine/ivmodelinfo.h
	../../public/tier1/KeyValues.h
	../../public/tier0/l2cache.h
	../../common/language.h
	logicrelay.h
	../../public/map_utils.h
	mapentities.h
	../shared/mapentities_shared.h
	../../public/tier0/mem.h
	../../public/tier0/memalloc.h
	../../public/tier0/memdbgoff.h
	../../public/tier0/memdbgon.h
	modelentities.h
	../shared/movevars_shared.h
	../shared/mp_shareddefs.h
	../../public/networkvar.h
	npc_vehicledriver.h
	../shared/npcevent.h
	../../public/vphysics/object_hash.h
	particle_system.h
	physics_cannister.h
	physics_fx.h
	physics_impact_damage.h
	../../public/tier0/platform.h
	../../public/vphysics/player_controller.h
	playerinfomanager.h
	../shared/playernet_vars.h
	../../public/PlayerState.h
	../shared/precipitation_shared.h
	../shared/predictable_entity.h
	../shared/predictioncopy.h
	../../public/tier1/processor_detect.h
	../shared/props_shared.h
	../../public/tier0/protected_things.h
	../shared/querycache.h
	../../public/vstdlib/random.h
	../shared/rope_helpers.h
	../shared/saverestore_stringtable.h
	../shared/saverestore_utlclass.h
	../shared/saverestore_utlmap.h
	../shared/saverestore_utlrbtree.h
	../../public/saverestoretypes.h
	../../public/scratchpad3d.h
	scratchpad_gamedll_helpers.h
	../../public/ScratchPadUtils.h
	sendproxy.h
	../../public/shake.h
	../shared/shared_classnames.h
	../shared/shareddefs.h
	../shared/sharedInterface.h
	../shared/shot_manipulator.h
	SkyCamera.h
	../../public/soundchars.h
	../shared/soundenvelope.h
	../../public/soundflags.h
	soundscape_system.h
	../../public/stdstring.h
	../../public/string_t.h
	../../public/tier1/stringpool.h
	../../public/tier1/strtools.h
	../../public/studio.h
	../shared/sun_shared.h
	../shared/takedamageinfo.h
	te_effect_dispatch.h
	tesla.h
	test_stressentities.h
	textstatsmgr.h
	../../public/texture_group_names.h
	timedeventmgr.h
	../shared/usercmd.h
	../shared/usermessages.h
	../shared/util_shared.h
	../../public/UtlCachedFileData.h
	../../public/tier1/utldict.h
	../../public/tier1/utlfixedmemory.h
	../../public/tier1/utlhash.h
	../../public/tier1/utllinkedlist.h
	../../public/tier1/utlmap.h
	../../public/tier1/utlmemory.h
	../../public/tier1/utlmultilist.h
	../../public/tier1/utlpriorityqueue.h
	../../public/tier1/utlrbtree.h
	../../public/tier1/UtlSortVector.h
	../../public/tier1/utlvector.h
	../../public/vallocator.h
	variant_t.h
	../../public/vcollide.h
	../../public/vcollide_parse.h
	../../public/tier0/vcr_shared.h
	../../public/tier0/vcrmode.h
	../../public/mathlib/vector.h
	../../public/mathlib/vector2d.h
	../../public/mathlib/vector4d.h
	vehicle_base.h
	vehicle_baseserver.h
	../shared/vehicle_viewblend_shared.h
	../../public/vphysics/vehicles.h
	../../public/vgui/VGUI.h
	../../public/vphysics_interface.h
	../shared/vphysics_sound.h
	../../public/mathlib/vplane.h
	../../public/tier0/vprof.h
	../../public/vstdlib/vstdlib.h
	../../public/winlite.h
	../../public/worldsize.h
	../../public/zip_uncompressed.h
	../../common/replay/ireplaysessionrecorder.h
	../shared/achievement_saverestore.h
	../shared/achievementmgr.h
	../shared/activitylist.h
	../shared/ai_activity.h
	ai_baseactor.h
	ai_basehumanoid.h
	ai_basenpc.h
	ai_basenpc_flyer.h
	ai_basenpc_flyer_new.h
	ai_basenpc_physicsflyer.h
	ai_behavior.h
	ai_behavior_assault.h
	ai_behavior_fear.h
	ai_behavior_follow.h
	ai_behavior_lead.h
	ai_behavior_rappel.h
	ai_behavior_standoff.h
	ai_blended_movement.h
	ai_component.h
	ai_condition.h
	AI_Criteria.h
	ai_debug.h
	../shared/ai_debug_shared.h
	ai_default.h
	ai_dynamiclink.h
	ai_eventresponse.h
	ai_goalentity.h
	ai_hint.h
	ai_hull.h
	ai_initutils.h
	AI_Interest_Target.h
	ai_link.h
	ai_localnavigator.h
	ai_looktarget.h
	ai_memory.h
	ai_motor.h
	ai_moveprobe.h
	ai_moveshoot.h
	ai_movesolver.h
	ai_movetypes.h
	ai_namespaces.h
	ai_navgoaltype.h
	ai_navigator.h
	ai_navtype.h
	ai_network.h
	ai_networkmanager.h
	ai_node.h
	ai_npcstate.h
	ai_obstacle_type.h
	ai_pathfinder.h
	ai_planesolver.h
	ai_playerally.h
	AI_ResponseSystem.h
	ai_route.h
	ai_routedist.h
	ai_saverestore.h
	ai_schedule.h
	ai_scriptconditions.h
	ai_senses.h
	ai_sentence.h
	ai_speech.h
	ai_speechfilter.h
	ai_squad.h
	ai_squadslot.h
	ai_tacticalservices.h
	ai_task.h
	ai_trackpather.h
	ai_utils.h
	ai_waypoint.h
	../shared/animation.h
	../shared/apparent_velocity_helper.h
	../shared/baseachievement.h
	baseanimating.h
	BaseAnimatingOverlay.h
	basecombatcharacter.h
	basecombatweapon.h
	../shared/basecombatweapon_shared.h
	baseentity.h
	../shared/baseentity_shared.h
	baseflex.h
	../shared/basegrenade_shared.h
	basemultiplayerplayer.h
	../shared/baseparticleentity.h
	../shared/baseplayer_shared.h
	BasePropDoor.h
	basetoggle.h
	baseviewmodel.h
	../shared/baseviewmodel_shared.h
	../shared/beam_shared.h
	bitstring.h
	../../public/bone_setup.h
	buttons.h
	cbase.h
	../shared/choreoactor.h
	../shared/choreochannel.h
	../shared/choreoevent.h
	../shared/choreoscene.h
	client.h
	../shared/collisionproperty.h
	../../public/collisionutils.h
	CRagdollMagnet.h
	../shared/debugoverlay_shared.h
	doors.h
	../../public/edict.h
	../../public/editor_sendcommand.h
	../shared/effect_color_tables.h
	effects.h
	../../public/eiface.h
	enginecallback.h
	entityapi.h
	entityblocker.h
	EntityDissolve.h
	entityinput.h
	entitylist.h
	entityoutput.h
	EntityParticleTrail.h
	../shared/entityparticletrail_shared.h
	env_debughistory.h
	env_player_surface_trigger.h
	../shared/env_wind_shared.h
	env_zoom.h
	EnvLaser.h
	EnvMessage.h
	envmicrophone.h
	envspark.h
	../../public/event_flags.h
	event_tempentity_tester.h
	../shared/eventlist.h
	eventqueue.h
	explode.h
	filters.h
	fire.h
	fire_smoke.h
	fish.h
	fourwheelvehiclephysics.h
	func_areaportalbase.h
	func_areaportalwindow.h
	func_break.h
	func_breakablesurf.h
	../shared/func_dust_shared.h
	func_movelinear.h
	game.h
	gameinterface.h
	../shared/gamemovement.h
	../shared/gamerules.h
	../shared/gamestats.h
	../shared/gamestringpool.h
	../shared/gamevars_shared.h
	gameweaponmanager.h
	gib.h
	globalstate.h
	globalstate_private.h
	grenadethrown.h
	h_cycler.h
	hierarchy.h
	../shared/hintmessage.h
	../shared/hintsystem.h
	../../common/hl2orange.spa.h
	hltvdirector.h
	../shared/ichoreoeventcallback.h
	../shared/igamesystem.h
	info_camera_link.h
	init_factory.h
	../../public/interpolatortypes.h
	../shared/interval.h
	../../public/iregistry.h
	../shared/iscenetokenprocessor.h
	iservervehicle.h
	items.h
	../../public/ivoiceserver.h
	../../public/keyframe/keyframe.h
	lights.h
	locksounds.h
	maprules.h
	../../public/mathlib/mathlib.h
	../../public/model_types.h
	monstermaker.h
	movehelper_server.h
	movie_explosion.h
	../shared/multiplay_gamerules.h
	ndebugoverlay.h
	networkstringtable_gamedll.h
	../../public/networkstringtabledefs.h
	../shared/obstacle_pushaway.h
	particle_fire.h
	particle_light.h
	../shared/particle_parse.h
	particle_smokegrenade.h
	pathtrack.h
	../../public/vphysics/performance.h
	phys_controller.h
	physconstraint.h
	physics.h
	physics_bone_follower.h
	physics_collisionevent.h
	physics_npc_solver.h
	physics_prop_ragdoll.h
	../shared/physics_saverestore.h
	../shared/physics_shared.h
	physobj.h
	player.h
	player_command.h
	player_pickup.h
	player_resource.h
	playerlocaldata.h
	../shared/point_bonusmaps_accessor.h
	point_camera.h
	../shared/point_posecontroller.h
	point_template.h
	../../public/mathlib/polyhedron.h
	../shared/positionwatcher.h
	../shared/precache_register.h
	../shared/predictableid.h
	props.h
	pushentity.h
	../shared/ragdoll_shared.h
	RagdollBoogie.h
	recipientfilter.h
	rope.h
	../../public/rope_physics.h
	../../public/rope_shared.h
	../shared/saverestore.h
	../shared/saverestore_bitstring.h
	../shared/saverestore_utlsymbol.h
	../shared/saverestore_utlvector.h
	sceneentity.h
	scripted.h
	scriptedtarget.h
	../shared/scriptevent.h
	../../public/server_class.h
	../server/serverbenchmark_base.h
	ServerNetworkProperty.h
	../shared/SharedFunctorUtils.h
	../../public/shattersurfacetypes.h
	../shared/sheetsimulator.h
	../../public/simple_physics.h
	../shared/simtimer.h
	../shared/singleplay_gamerules.h
	../shared/solidsetdefaults.h
	soundent.h
	soundscape.h
	spark.h
	spotlightend.h
	../shared/Sprite.h
	../shared/SpriteTrail.h
	../../public/vphysics/stats.h
	../../public/steam/steam_api.h
	../../public/stringregistry.h
	tactical_mission.h
	team.h
	team_spawnpoint.h
	../shared/teamplay_gamerules.h
	../shared/tempentity.h
	TemplateEntities.h
	../shared/touchlink.h
	trains.h
	triggers.h
	util.h
	../shared/vehicle_choreo_generic_shared.h
	vehicle_sounds.h
	vguiscreen.h
	../../public/mathlib/vmatrix.h
	../shared/voice_common.h
	../shared/voice_gamemgr.h
	../server/vote_controller.h
	waterbullet.h
	wcedit.h
	../shared/weapon_parse.h
	../shared/weapon_proficiency.h
	world.h
	hl2/ai_behavior_actbusy.h
	episodic/ai_behavior_alyx_injured.h
	hl2/ai_behavior_functank.h
	hl2/ai_behavior_holster.h
	hl2/ai_behavior_operator.h
	ai_behavior_passenger.h
	episodic/ai_behavior_passenger_companion.h
	episodic/ai_behavior_passenger_zombie.h
	hl2/ai_behavior_police.h
	hl2/ai_goal_police.h
	hl2/ai_interactions.h
	hl2/ai_spotlight.h
	hl2/antlion_dust.h
	hl2/antlion_maker.h
	hl2/ar2_explosion.h
	basebludgeonweapon.h
	hl2/basehlcombatweapon.h
	../shared/hl2/basehlcombatweapon_shared.h
	hl2/cbasehelicopter.h
	hl2/cbasespriteprojectile.h
	../shared/hl2/citadel_effects_shared.h
	hl2/combine_mine.h
	hl2/energy_wave.h
	../shared/hl2/env_alyxemp_shared.h
	../shared/hl2/env_headcrabcanister_shared.h
	hl2/func_bulletshield.h
	hl2/func_tank.h
	hl2/grenade_ar2.h
	hl2/grenade_bugbait.h
	hl2/grenade_frag.h
	hl2/grenade_spit.h
	../shared/hl2/hl2_gamerules.h
	hl2/hl2_player.h
	../shared/hl2/hl2_player_shared.h
	hl2/hl2_playerlocaldata.h
	../shared/hl2/hl2_shareddefs.h
	../shared/hl2/hl_gamemovement.h
	../shared/hl2/hl_movedata.h
	hl2/info_darknessmode_lightsource.h
	hl2/item_dynamic_resupply.h
	../shared/episodic/npc_advisor_shared.h
	hl2/npc_alyx_episodic.h
	hl2/npc_antlion.h
	hl2/npc_attackchopper.h
	hl2/npc_barnacle.h
	hl2/npc_basescanner.h
	hl2/npc_BaseZombie.h
	hl2/npc_bullseye.h
	hl2/npc_citizen17.h
	hl2/npc_combine.h
	hl2/npc_combines.h
	hl2/npc_crow.h
	hl2/npc_headcrab.h
	episodic/npc_hunter.h
	hl2/npc_manhack.h
	hl2/npc_metropolice.h
	hl2/npc_playercompanion.h
	hl2/npc_rollermine.h
	hl2/npc_scanner.h
	hl2/npc_stalker.h
	hl2/npc_strider.h
	npc_talker.h
	hl2/npc_vortigaunt_episodic.h
	hl2/prop_combine_ball.h
	hl2/rotorwash.h
	hl2/script_intro.h
	hl2/vehicle_apc.h
	hl2/vehicle_crane.h
	episodic/vehicle_jeep_episodic.h
	hl2/weapon_alyxgun.h
	hl2/weapon_ar2.h
	hl2/weapon_citizenpackage.h
	hl2/weapon_crowbar.h
	hl2/weapon_physcannon.h
	hl2/weapon_rpg.h
	episodic/weapon_striderbuster.h
	hl2/weapon_stunstick.h
	hl2/grenade_beam.h
	hl2/grenade_homer.h
	hl2/grenade_pathfollower.h
	hl2/weapon_flaregun.h
	plasma.h
	smoke_trail.h
	smokestack.h
	steamjet.h
	te.h
	te_basebeam.h
	te_particlesystem.h
	toolframework_server.h

	bla/timer.cpp
	gamedll_replay.cpp
	../shared/achievement_saverestore.cpp
	../shared/achievementmgr.cpp
	../shared/achievements_hlx.cpp
	../shared/activitylist.cpp
	ai_activity.cpp
	ai_baseactor.cpp
	ai_basehumanoid.cpp
	ai_basenpc.cpp
	ai_basenpc_flyer.cpp
	ai_basenpc_flyer_new.cpp
	ai_basenpc_movement.cpp
	ai_basenpc_physicsflyer.cpp
	ai_basenpc_schedule.cpp
	ai_basenpc_squad.cpp
	ai_behavior.cpp
	ai_behavior_assault.cpp
	ai_behavior_fear.cpp
	ai_behavior_follow.cpp
	ai_behavior_lead.cpp
	ai_behavior_rappel.cpp
	ai_behavior_standoff.cpp
	ai_blended_movement.cpp
	ai_concommands.cpp
	ai_condition.cpp
	AI_Criteria.cpp
	ai_default.cpp
	ai_dynamiclink.cpp
	ai_event.cpp
	ai_eventresponse.cpp
	ai_goalentity.cpp
	ai_hint.cpp
	ai_hull.cpp
	ai_initutils.cpp
	AI_Interest_Target.cpp
	ai_link.cpp
	ai_localnavigator.cpp
	ai_looktarget.cpp
	ai_memory.cpp
	ai_motor.cpp
	ai_moveprobe.cpp
	ai_moveshoot.cpp
	ai_movesolver.cpp
	ai_namespaces.cpp
	ai_navigator.cpp
	ai_network.cpp
	ai_networkmanager.cpp
	ai_node.cpp
	ai_pathfinder.cpp
	ai_planesolver.cpp
	ai_playerally.cpp
	ai_relationship.cpp
	AI_ResponseSystem.cpp
	ai_route.cpp
	ai_saverestore.cpp
	ai_schedule.cpp
	ai_scriptconditions.cpp
	ai_senses.cpp
	ai_sentence.cpp
	ai_speech.cpp
	ai_speechfilter.cpp
	ai_squad.cpp
	ai_squadslot.cpp
	ai_tacticalservices.cpp
	ai_task.cpp
	ai_trackpather.cpp
	ai_utils.cpp
	ai_waypoint.cpp
	../shared/ammodef.cpp
	../shared/animation.cpp
	base_gameinterface.cpp
	../shared/base_playeranimstate.cpp
	base_transmit_proxy.cpp
	../shared/baseachievement.cpp
	baseanimating.cpp
	BaseAnimatingOverlay.cpp
	basecombatcharacter.cpp
	../shared/basecombatcharacter_shared.cpp
	basecombatweapon.cpp
	../shared/basecombatweapon_shared.cpp
	baseentity.cpp
	../shared/baseentity_shared.cpp
	baseflex.cpp
	basegrenade_concussion.cpp
	basegrenade_contact.cpp
	../shared/basegrenade_shared.cpp
	basegrenade_timed.cpp
	basemultiplayerplayer.cpp
	../shared/baseparticleentity.cpp
	../shared/baseplayer_shared.cpp
	baseviewmodel.cpp
	../shared/baseviewmodel_shared.cpp
	../shared/beam_shared.cpp
	bitstring.cpp
	bmodels.cpp
	../../public/bone_setup.cpp
	buttons.cpp
	cbase.cpp
	client.cpp
	../shared/collisionproperty.cpp
	../../public/collisionutils.cpp
	colorcorrection.cpp
	colorcorrectionvolume.cpp
	CommentarySystem.cpp
	controlentities.cpp
	cplane.cpp
	CRagdollMagnet.cpp
	damagemodifier.cpp
	../shared/death_pose.cpp
	../shared/debugoverlay_shared.cpp
	../shared/decals.cpp
	doors.cpp
	../../public/dt_send.cpp
	../../public/dt_utlvector_common.cpp
	../../public/dt_utlvector_send.cpp
	dynamiclight.cpp
	../../public/editor_sendcommand.cpp
	../shared/effect_dispatch_data.cpp
	effects.cpp
	EffectsServer.cpp
	../shared/ehandle.cpp
	entityblocker.cpp
	EntityDissolve.cpp
	EntityFlame.cpp
	entitylist.cpp
	../shared/entitylist_base.cpp
	EntityParticleTrail.cpp
	../shared/EntityParticleTrail_Shared.cpp
	env_debughistory.cpp
	../shared/env_detail_controller.cpp
	env_effectsscript.cpp
	env_entity_maker.cpp
	env_particlescript.cpp
	env_player_surface_trigger.cpp
	env_projectedtexture.cpp
	env_screenoverlay.cpp
	env_texturetoggle.cpp
	env_tonemap_controller.cpp
	../shared/env_wind_shared.cpp
	env_zoom.cpp
	EnvBeam.cpp
	EnvFade.cpp
	EnvHudHint.cpp
	EnvLaser.cpp
	EnvMessage.cpp
	envmicrophone.cpp
	EnvShake.cpp
	EnvSpark.cpp
	../shared/eventlist.cpp
	EventLog.cpp
	explode.cpp
	../../public/filesystem_helpers.cpp
	filters.cpp
	fire.cpp
	fire_smoke.cpp
	fish.cpp
	fogcontroller.cpp
	fourwheelvehiclephysics.cpp
	func_areaportal.cpp
	func_areaportalbase.cpp
	func_areaportalwindow.cpp
	func_break.cpp
	func_breakablesurf.cpp
	func_dust.cpp
	../shared/func_ladder.cpp
	func_ladder_endpoint.cpp
	func_lod.cpp
	func_movelinear.cpp
	func_occluder.cpp
	func_reflective_glass.cpp
	func_smokevolume.cpp
	game.cpp
	game_ui.cpp
	gamehandle.cpp
	gameinterface.cpp
	../shared/gamemovement.cpp
	../shared/gamerules.cpp
	../shared/gamerules_register.cpp
	../shared/GameStats.cpp
	GameStats_BasicStatsFunctions.cpp
	../shared/gamestringpool.cpp
	gametrace_dll.cpp
	../shared/gamevars_shared.cpp
	gameweaponmanager.cpp
	genericactor.cpp
	genericmonster.cpp
	gib.cpp
	globals.cpp
	globalstate.cpp
	grenadethrown.cpp
	guntarget.cpp
	hl2/prop_gravity_ball.cpp
	h_ai.cpp
	h_cycler.cpp
	h_export.cpp
	../../public/haptics/haptic_msgs.cpp
	../../public/haptics/haptic_utils.cpp
	hierarchy.cpp
	../shared/hintmessage.cpp
	../shared/hintsystem.cpp
	hltvdirector.cpp
	../shared/igamesystem.cpp
	info_camera_link.cpp
	info_overlay_accessor.cpp
	init_factory.cpp
	intermission.cpp
	../../public/interpolatortypes.cpp
	../shared/interval.cpp
	item_world.cpp
	../../public/keyframe/keyframe.cpp
	../../common/language.cpp
	lightglow.cpp
	lights.cpp
	logic_achievement.cpp
	logic_measure_movement.cpp
	logic_navigation.cpp
	logicauto.cpp
	logicentities.cpp
	logicrelay.cpp
	../../public/map_utils.cpp
	mapentities.cpp
	../shared/mapentities_shared.cpp
	maprules.cpp
	MaterialModifyControl.cpp
	../../public/tier0/memoverride.cpp
	message_entity.cpp
	modelentities.cpp
	../shared/ModelSoundsCache.cpp
	monstermaker.cpp
	movehelper_server.cpp
	movement.cpp
	../shared/movevars_shared.cpp
	../shared/mp_shareddefs.cpp
	../shared/multiplay_gamerules.cpp
	ndebugoverlay.cpp
	../../public/networkvar.cpp
	npc_vehicledriver.cpp
	../shared/obstacle_pushaway.cpp
	particle_light.cpp
	../shared/particle_parse.cpp
	particle_system.cpp
	../shared/particlesystemquery.cpp
	pathcorner.cpp
	pathtrack.cpp
	phys_controller.cpp
	physconstraint.cpp
	physics.cpp
	physics_bone_follower.cpp
	physics_cannister.cpp
	physics_fx.cpp
	physics_impact_damage.cpp
	physics_main.cpp
	../shared/physics_main_shared.cpp
	physics_npc_solver.cpp
	physics_prop_ragdoll.cpp
	../shared/physics_saverestore.cpp
	../shared/physics_shared.cpp
	physobj.cpp
	player.cpp
	player_command.cpp
	player_lagcompensation.cpp
	player_pickup.cpp
	player_resource.cpp
	playerinfomanager.cpp
	playerlocaldata.cpp
	plugin_check.cpp
	../shared/point_bonusmaps_accessor.cpp
	point_camera.cpp
	point_devshot_camera.cpp
	point_playermoveconstraint.cpp
	../shared/point_posecontroller.cpp
	point_spotlight.cpp
	point_template.cpp
	pointanglesensor.cpp
	PointAngularVelocitySensor.cpp
	pointhurt.cpp
	pointteleport.cpp
	../shared/precache_register.cpp
	../shared/predictableid.cpp
	props.cpp
	../shared/props_shared.cpp
	../shared/querycache.cpp
	ragdoll_manager.cpp
	../shared/ragdoll_shared.cpp
	RagdollBoogie.cpp
	../../common/randoverride.cpp
	recipientfilter.cpp
	../../public/registry.cpp
	rope.cpp
	../shared/rope_helpers.cpp
	../../public/rope_physics.cpp
	../shared/saverestore.cpp
	saverestore_gamedll.cpp
	../shared/SceneCache.cpp
	sceneentity.cpp
	../shared/sceneentity_shared.cpp
	../../public/scratchpad3d.cpp
	scratchpad_gamedll_helpers.cpp
	../../public/ScratchPadUtils.cpp
	scripted.cpp
	scriptedtarget.cpp
	sendproxy.cpp
	../shared/sequence_Transitioner.cpp
	../../public/server_class.cpp
	../server/serverbenchmark_base.cpp
	ServerNetworkProperty.cpp
	shadowcontrol.cpp
	../shared/sheetsimulator.cpp
	../../public/simple_physics.cpp
	../shared/simtimer.cpp
	../shared/singleplay_gamerules.cpp
	SkyCamera.cpp
	slideshow_display.cpp
	sound.cpp
	../shared/SoundEmitterSystem.cpp
	soundent.cpp
	../shared/soundenvelope.cpp
	../../public/SoundParametersInternal.cpp
	soundscape.cpp
	soundscape_system.cpp
	spotlightend.cpp
	../shared/Sprite.cpp
	sprite_perfmonitor.cpp
	../../public/stringregistry.cpp
	../../public/studio.cpp
	../shared/studio_shared.cpp
	subs.cpp
	sun.cpp
	../shared/hl2/survival_gamerules.cpp
	tactical_mission.cpp
	../shared/takedamageinfo.cpp
	tanktrain.cpp
	team.cpp
	team_spawnpoint.cpp
	../shared/teamplay_gamerules.cpp
	TemplateEntities.cpp
	tempmonster.cpp
	tesla.cpp
	../shared/test_ehandle.cpp
	test_proxytoggle.cpp
	test_stressentities.cpp
	testfunctions.cpp
	testtraceline.cpp
	textstatsmgr.cpp
	timedeventmgr.cpp
	trains.cpp
	triggers.cpp
	../shared/usercmd.cpp
	util.cpp
	../shared/util_shared.cpp
	variant_t.cpp
	vehicle_base.cpp
	vehicle_baseserver.cpp
	vehicle_choreo_generic.cpp
	../shared/vehicle_viewblend_shared.cpp
	vguiscreen.cpp
	../shared/voice_gamemgr.cpp
	../server/vote_controller.cpp
	waterbullet.cpp
	WaterLODControl.cpp
	wcedit.cpp
	../shared/weapon_parse.cpp
	../shared/weapon_parse_default.cpp
	../shared/weapon_proficiency.cpp
	weight_button.cpp
	world.cpp
	../shared/episodic/achievements_ep1.cpp
	../shared/episodic/achievements_ep2.cpp
	../shared/episodic/achievements_epx.cpp
	hl2/ai_allymanager.cpp
	hl2/ai_behavior_actbusy.cpp
	episodic/ai_behavior_alyx_injured.cpp
	hl2/ai_behavior_functank.cpp
	hl2/ai_behavior_holster.cpp
	hl2/ai_behavior_operator.cpp
	ai_behavior_passenger.cpp
	episodic/ai_behavior_passenger_companion.cpp
	episodic/ai_behavior_passenger_zombie.cpp
	hl2/ai_behavior_police.cpp
	hl2/ai_goal_police.cpp
	hl2/ai_spotlight.cpp
	hl2/antlion_dust.cpp
	hl2/antlion_maker.cpp
	hl2/ar2_explosion.cpp
	basebludgeonweapon.cpp
	hl2/basehlcombatweapon.cpp
	../shared/hl2/basehlcombatweapon_shared.cpp
	hl2/cbasehelicopter.cpp
	hl2/cbasespriteprojectile.cpp
	hl2/citadel_effects.cpp
	hl2/combine_mine.cpp
	hl2/env_alyxemp.cpp
	hl2/env_headcrabcanister.cpp
	../shared/hl2/env_headcrabcanister_shared.cpp
	hl2/env_speaker.cpp
	hl2/env_starfield.cpp
	hl2/func_bulletshield.cpp
	hl2/Func_Monitor.cpp
	hl2/func_recharge.cpp
	hl2/func_tank.cpp
	hl2/grenade_ar2.cpp
	hl2/grenade_bugbait.cpp
	hl2/grenade_frag.cpp
	hl2/grenade_spit.cpp
	hl2/hl2_ai_network.cpp
	hl2/hl2_client.cpp
	hl2/hl2_eventlog.cpp
	../shared/hl2/hl2_gamerules.cpp
	hl2/hl2_player.cpp
	hl2/hl2_playerlocaldata.cpp
	hl2/hl2_triggers.cpp
	../shared/hl2/hl2_usermessages.cpp
	../shared/hl2/hl_gamemovement.cpp
	hl2/hl_playermove.cpp
	hl2/info_darknessmode_lightsource.cpp
	hl2/info_teleporter_countdown.cpp
	hl2/item_ammo.cpp
	hl2/item_battery.cpp
	hl2/item_dynamic_resupply.cpp
	hl2/item_healthkit.cpp
	hl2/item_itemcrate.cpp
	hl2/item_suit.cpp
	hl2/look_door.cpp
	hl2/monster_dummy.cpp
	episodic/npc_advisor.cpp
	hl2/npc_alyx_episodic.cpp
	hl2/npc_antlion.cpp
	hl2/npc_antliongrub.cpp
	hl2/npc_antlionguard.cpp
	hl2/npc_apcdriver.cpp
	hl2/npc_attackchopper.cpp
	hl2/npc_barnacle.cpp
	hl2/npc_barney.cpp
	hl2/npc_basescanner.cpp
	hl2/npc_BaseZombie.cpp
	hl2/npc_breen.cpp
	hl2/npc_bullseye.cpp
	hl2/npc_citizen17.cpp
	hl2/npc_combine.cpp
	episodic/npc_combine_cannon.cpp
	hl2/npc_combinecamera.cpp
	hl2/npc_combinedropship.cpp
	hl2/npc_combinegunship.cpp
	hl2/npc_combines.cpp
	hl2/npc_cranedriver.cpp
	hl2/npc_crow.cpp
	hl2/npc_dog.cpp
	hl2/npc_eli.cpp
	hl2/npc_enemyfinder.cpp
	hl2/npc_fastzombie.cpp
	hl2/npc_fisherman.cpp
	hl2/npc_gman.cpp
	hl2/npc_headcrab.cpp
	episodic/npc_hunter.cpp
	hl2/npc_ichthyosaur.cpp
	hl2/npc_kleiner.cpp
	hl2/npc_launcher.cpp
	episodic/npc_magnusson.cpp
	hl2/npc_manhack.cpp
	hl2/npc_metropolice.cpp
	hl2/npc_monk.cpp
	hl2/npc_mossman.cpp
	hl2/npc_playercompanion.cpp
	hl2/npc_PoisonZombie.cpp
	episodic/npc_puppet.cpp
	hl2/npc_rollermine.cpp
	hl2/npc_scanner.cpp
	hl2/npc_stalker.cpp
	hl2/npc_strider.cpp
	npc_talker.cpp
	hl2/npc_turret_ceiling.cpp
	hl2/npc_turret_floor.cpp
	hl2/npc_turret_ground.cpp
	hl2/npc_vortigaunt_episodic.cpp
	hl2/npc_zombie.cpp
	hl2/npc_zombine.cpp
	hl2/point_apc_controller.cpp
	hl2/prop_combine_ball.cpp
	episodic/prop_scalable.cpp
	hl2/prop_thumper.cpp
	hl2/proto_sniper.cpp
	hl2/rotorwash.cpp
	hl2/script_intro.cpp
	../shared/script_intro_shared.cpp
	hl2/vehicle_airboat.cpp
	hl2/vehicle_cannon.cpp
	hl2/vehicle_crane.cpp
	hl2/vehicle_jeep.cpp
	episodic/vehicle_jeep_episodic.cpp
	hl2/vehicle_prisoner_pod.cpp
	hl2/vehicle_viewcontroller.cpp
	hl2/weapon_357.cpp
	hl2/weapon_alyxgun.cpp
	hl2/weapon_annabelle.cpp
	hl2/weapon_ar2.cpp
	hl2/weapon_bugbait.cpp
	hl2/weapon_citizenpackage.cpp
	hl2/weapon_crossbow.cpp
	hl2/weapon_crowbar.cpp
	weapon_cubemap.cpp
	hl2/weapon_frag.cpp
	hl2/weapon_physcannon.cpp
	hl2/weapon_pistol.cpp
	hl2/weapon_rpg.cpp
	hl2/weapon_shotgun.cpp
	hl2/weapon_smg1.cpp
	episodic/weapon_striderbuster.cpp
	hl2/weapon_stunstick.cpp
	hl2/grenade_beam.cpp
	hl2/grenade_homer.cpp
	hl2/grenade_pathfollower.cpp
	hl2/npc_missiledefense.cpp
	hl2/vehicle_apc.cpp
	hl2/weapon_cguard.cpp
	hl2/weapon_flaregun.cpp
	stdafx.cpp
	basetempentity.cpp
	event_tempentity_tester.cpp
	movie_explosion.cpp
	particle_fire.cpp
	particle_smokegrenade.cpp
	plasma.cpp
	smoke_trail.cpp
	smokestack.cpp
	../shared/SpriteTrail.cpp
	steamjet.cpp
	te.cpp
	te_armorricochet.cpp
	te_basebeam.cpp
	te_beamentpoint.cpp
	te_beaments.cpp
	te_beamfollow.cpp
	te_beamlaser.cpp
	te_beampoints.cpp
	te_beamring.cpp
	te_beamringpoint.cpp
	te_beamspline.cpp
	te_bloodsprite.cpp
	te_bloodstream.cpp
	te_breakmodel.cpp
	te_bspdecal.cpp
	te_bubbles.cpp
	te_bubbletrail.cpp
	te_clientprojectile.cpp
	te_decal.cpp
	te_dynamiclight.cpp
	te_effect_dispatch.cpp
	te_energysplash.cpp
	te_explosion.cpp
	te_fizz.cpp
	te_footprintdecal.cpp
	hl2/te_gaussexplosion.cpp
	te_glassshatter.cpp
	te_glowsprite.cpp
	te_impact.cpp
	te_killplayerattachments.cpp
	te_largefunnel.cpp
	te_muzzleflash.cpp
	te_particlesystem.cpp
	te_physicsprop.cpp
	te_playerdecal.cpp
	te_projecteddecal.cpp
	te_showline.cpp
	te_smoke.cpp
	te_sparks.cpp
	te_sprite.cpp
	te_spritespray.cpp
	te_worlddecal.cpp
	../shared/usermessages.cpp
	entity_tools_server.cpp
	toolframework_server.cpp


	${BLAMOD_FW_FILES}

	../shared/hl2/weapon_brgauss.cpp
)

target_link_libraries(server
	tier1

	choreoobjects
	dmxloader
	mathlib
	particles
	steam_api
	tier0
	tier2
	tier3
	vstdlib
)

install(
	TARGETS server 
	RUNTIME
	DESTINATION blamod/bin
)