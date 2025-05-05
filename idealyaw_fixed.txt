--==[ IdealYaw Combined Script ]==--

--==[ idealyaw_builder.lua ]==--
 local L0 = require 'ffi'
local L1 = require 'bit'
local L2 = require "vector"
local L3 = require "gamesense/antiaim_funcs" or error "https://gamesense.pub/forums/viewtopic.php?id=29665"
local L4 = require "gamesense/surface"
local L5 = require "gamesense/base64" or error("Base64 library required")
local L6 = require "gamesense/clipboard" or error("Clipboard library required")
local L7, L8, L9, L10, L11, L12, L13, L14, L15 = require, pcall, ipairs, pairs, unpack, tonumber, tostring, toticks, totime;
local L16 = { new = L0.new, typeof = L0.typeof, cast = L0.cast, cdef = L0.cdef, sizeof = L0.sizeof, string = L0.string }
local L17 = { loadstring = panorama.loadstring, open = panorama.open }
local L18 = { get = plist.get, set = plist.set }
local L19 = { export = config.export, import = config.import, load = config.load }
local L20 = { flush = database.flush, read = database.read, write = database.write }
local L21 = { arshift = L1.arshift, band = L1.band, bnot = L1.bnot, bor = L1.bor, bswap = L1.bswap, bxor = L1.bxor, lshift = L1.lshift, rol = L1.rol, ror = L1.ror, rshift = L1.rshift, tobit = L1.tobit, tohex = L1.tohex }
local L22 = { byte = string.byte, char = string.char, find = string.find, format = string.format, gmatch = string.gmatch, gsub = string.gsub, len = string.len, lower = string.lower, match = string.match, rep = string.rep, reverse = string.reverse, sub = string.sub, upper = string.upper }
local L23 = { abs = math.abs, acos = math.acos, asin = math.asin, atan = math.atan, atan2 = math.atan2, ceil = math.ceil, cos = math.cos, cosh = math.cosh, deg = math.deg, exp = math.exp, floor = math.floor, fmod = math.fmod, frexp = math.frexp, ldexp = math.ldexp, log = math.log, log10 = math.log10, max = math.max, min = math.min, modf = math.modf, pow = math.pow, rad = math.rad, random = math.random, randomseed = math.randomseed, sin = math.sin, sinh = math.sinh, sqrt = math.sqrt, tan = math.tan, tanh = math.tanh, pi = math.pi }
local L24 = { get = ui.get, is_menu_open = ui.is_menu_open, menu_size = ui.menu_size, menu_position = ui.menu_position, mouse_position = ui.mouse_position, name = ui.name, new_button = ui.new_button, new_checkbox = ui.new_checkbox, new_color_picker = ui.new_color_picker, new_combobox = ui.new_combobox, new_hotkey = ui.new_hotkey, new_label = ui.new_label, new_listbox = ui.new_listbox, new_multiselect = ui.new_multiselect, new_slider = ui.new_slider, new_string = ui.new_string, new_textbox = ui.new_textbox, reference = ui.reference, set = ui.set, set_callback = ui.set_callback, set_visible = ui.set_visible, update = ui.update }
local L25 = { blur = renderer.blur, circle = renderer.circle, circle_outline = renderer.circle_outline, gradient = renderer.gradient, indicator = renderer.indicator, line = renderer.line, load_jpg = renderer.load_jpg, load_png = renderer.load_png, load_rgba = renderer.load_rgba, load_svg = renderer.load_svg, measure_text = renderer.measure_text, rectangle = renderer.rectangle, text = renderer.text, texture = renderer.texture, triangle = renderer.triangle, world_to_screen = renderer.world_to_screen }
local L26 = { absoluteframetime = globals.absoluteframetime, chokedcommands = globals.chokedcommands, commandack = globals.commandack, curtime = globals.curtime, framecount = globals.framecount, frametime = globals.frametime, lastoutgoingcommand = globals.lastoutgoingcommand, mapname = globals.mapname, maxplayers = globals.maxplayers, oldcommandack = globals.oldcommandack, realtime = globals.realtime, tickcount = globals.tickcount, tickinterval = globals.tickinterval }
local L27 = { get_all = entity.get_all, get_bounding_box = entity.get_bounding_box, get_classname = entity.get_classname, get_esp_data = entity.get_esp_data, get_game_rules = entity.get_game_rules, get_local_player = entity.get_local_player, get_origin = entity.get_origin, get_player_name = entity.get_player_name, get_player_resource = entity.get_player_resource, get_player_weapon = entity.get_player_weapon, get_players = entity.get_players, get_prop = entity.get_prop, get_steam64 = entity.get_steam64, hitbox_position = entity.hitbox_position, is_alive = entity.is_alive, is_dormant = entity.is_dormant, is_enemy = entity.is_enemy, new_prop = entity.new_prop, set_prop = entity.set_prop }
local L28 = { camera_angles = _G.client.camera_angles, camera_position = _G.client.camera_position, color_log = _G.client.color_log, create_interface = _G.client.create_interface, current_threat = _G.client.current_threat, delay_call = _G.client.delay_call, draw_debug_text = _G.client.draw_debug_text, draw_hitboxes = _G.client.draw_hitboxes, error_log = _G.client.error_log, exec = _G.client.exec, eye_position = _G.client.eye_position, find_signature = _G.client.find_signature, fire_event = _G.client.fire_event, get_cvar = _G.client.get_cvar, get_model_name = _G.client.get_model_name, key_state = _G.client.key_state, latency = _G.client.latency, log = _G.client.log, random_float = _G.client.random_float, random_int = _G.client.random_int, real_latency = _G.client.real_latency, register_esp_flag = _G.client.register_esp_flag, reload_active_scripts = _G.client.reload_active_scripts, request_full_update = _G.client.request_full_update, scale_damage = _G.client.scale_damage, screen_size = _G.client.screen_size, set_clan_tag = _G.client.set_clan_tag, set_event_callback = _G.client.set_event_callback, system_time = _G.client.system_time, timestamp = _G.client.timestamp, trace_bullet = _G.client.trace_bullet, trace_line = _G.client.trace_line, unix_time = _G.client.unix_time, unset_event_callback = _G.client.unset_event_callback, update_player_list = _G.client.update_player_list, userid_to_entindex = _G.client.userid_to_entindex, visible = _G.client.visible }
local L29 = L16.typeof('void***')
local L30 = L28.create_interface('client.dll', 'VClientEntityList003') or error('VClientEntityList003 wasnt found', 2)
local L31 = L16.cast(L29, L30) or error('rawientitylist is nil', 2)
local L32 = L16.cast('void*(__thiscall*)(void*, int)', L31[0][3]) or error('get_client_entity is nil', 2)
local L33 = L16.cast('void*(__thiscall*)(void*, int)', L31[0][0]) or error('get_client_networkable_t is nil', 2)
L16.cdef([[
    struct animation_layer_t {
        char  pad_0000[20];
        uint32_t m_nOrder; //0x0014
        uint32_t m_nSequence; //0x0018
        float m_flPrevCycle; //0x001C
        float m_flWeight; //0x0020
        float m_flWeightDeltaRate; //0x0024
        float m_flPlaybackRate; //0x0028
        float m_flCycle; //0x002C
        void *m_pOwner; //0x0030 // player's thisptr
        char  pad_0038[4]; //0x0034
    };

    struct animstate_t1 {
        char pad[ 3 ];
        char m_bForceWeaponUpdate; //0x4
        char pad1[ 91 ];
        void* m_pBaseEntity; //0x60
        void* m_pActiveWeapon; //0x64
        void* m_pLastActiveWeapon; //0x68
        float m_flLastClientSideAnimationUpdateTime; //0x6C
        int m_iLastClientSideAnimationUpdateFramecount; //0x70
        float m_flAnimUpdateDelta; //0x74
        float m_flEyeYaw; //0x78
        float m_flPitch; //0x7C
        float m_flGoalFeetYaw; //0x80
        float m_flCurrentFeetYaw; //0x84
        float m_flCurrentTorsoYaw; //0x88
        float m_flUnknownVelocityLean; //0x8C
        float m_flLeanAmount; //0x90
        char pad2[ 4 ];
        float m_flFeetCycle; //0x98
        float m_flFeetYawRate; //0x9C
        char pad3[ 4 ];
        float m_fDuckAmount; //0xA4
        float m_fLandingDuckAdditiveSomething; //0xA8
        char pad4[ 4 ];
        float m_vOriginX; //0xB0
        float m_vOriginY; //0xB4
        float m_vOriginZ; //0xB8
        float m_vLastOriginX; //0xBC
        float m_vLastOriginY; //0xC0
        float m_vLastOriginZ; //0xC4
        float m_vVelocityX; //0xC8
        float m_vVelocityY; //0xCC
        char pad5[ 4 ];
        float m_flUnknownFloat1; //0xD4
        char pad6[ 8 ];
        float m_flUnknownFloat2; //0xE0
        float m_flUnknownFloat3; //0xE4
        float m_flUnknown; //0xE8
        float m_flSpeed2D; //0xEC
        float m_flUpVelocity; //0xF0
        float m_flSpeedNormalized; //0xF4
        float m_flFeetSpeedForwardsOrSideWays; //0xF8
        float m_flFeetSpeedUnknownForwardOrSideways; //0xFC
        float m_flTimeSinceStartedMoving; //0x100
        float m_flTimeSinceStoppedMoving; //0x104
        bool m_bOnGround; //0x108
        bool m_bInHitGroundAnimation; //0x109
        char m_pad[2];
        float m_flJumpToFall;
        float m_flTimeSinceInAir; //0x10A
        float m_flLastOriginZ; //0x10E
        float m_flHeadHeightOrOffsetFromHittingGroundAnimation; //0x112
        float m_flStopToFullRunningFraction; //0x116
        char pad7[ 4 ]; //0x11A
        float m_flMagicFraction; //0x11E
        char pad8[ 60 ]; //0x122
        float m_flWorldForce; //0x15E
        char pad9[ 462 ]; //0x162
        float m_flMaxYaw; //0x334
    };

]])
L20.write("current_clip_board_to_save", "")
local L34 = {}
local L35 = { { 'remove_search_path', '\x55\x8B\xEC\x81\xEC\xCC\xCC\xCC\xCC\x8B\x55\x08\x53\x8B\xD9', 'void(__thiscall*)(void*, const char*, const char*)' }, { 'remove_file', '\x55\x8B\xEC\x81\xEC\xCC\xCC\xCC\xCC\x8D\x85\xCC\xCC\xCC\xCC\x56\x50\x8D\x45\x0C', 'void(__thiscall*)(void*, const char*, const char*)' }, { 'find_next', '\x55\x8B\xEC\x83\xEC\x0C\x53\x8B\xD9\x8B\x0D\xCC\xCC\xCC\xCC', 'const char*(__thiscall*)(void*, int)' }, { 'find_is_directory', '\x55\x8B\xEC\x0F\xB7\x45\x08', 'bool(__thiscall*)(void*, int)' }, { 'find_close', '\x55\x8B\xEC\x53\x8B\x5D\x08\x85', 'void(__thiscall*)(void*, int)' }, { 'find_first', '\x55\x8B\xEC\x6A\x00\xFF\x75\x10\xFF\x75\x0C\xFF\x75\x08\xE8\xCC\xCC\xCC\xCC\x5D', 'const char*(__thiscall*)(void*, const char*, const char*, int*)' }, { 'get_current_directory', '\x55\x8B\xEC\x56\x8B\x75\x08\x56\xFF\x75\x0C', 'bool(__thiscall*)(void*, char*, int)' } }
local L36 = L7('ffi')
local function L37(L38, L39, L40, L41)
    local L42 = L28.create_interface(L38, L39) or error("invalid interface", 2)
    local L43 = L28.find_signature(L38, L40) or error("invalid signature", 2)
    local L44, L45 = L8(L36.typeof, L41)
    if not L44 then
        error(L45, 2)
    end;
    local L46 = L36.cast(L45, L43) or error("invalid typecast", 2)
    return function(...)
        return L46(L42, ...)
    end
end;
for L47 = 1, #L35 do
    local L48 = L35[L47]
    L34[L48[1]] = L37('filesystem_stdio.dll', 'VFileSystem017', L48[2], L48[3])
end;
local L49 = vtable_bind("filesystem_stdio.dll", "VFileSystem017", 11, "void(__thiscall*)(void*, const char*, const char*, int)")
local L50 = "idealyaw_CONFIGS"
local L51 = L16.typeof("char[128]")()
L34.get_current_directory(L51, L16.sizeof(L51))
local L52 = L22.format('%s', L16.string(L51))
L49(L52, L50, 0)
local function L53()
    local L54, L55 = {}, L16.typeof("int[1]")()
    local L56 = L34.find_first("*", L50, L55)
    while L56 ~= nil do
        local L57 = L16.string(L56)
        if not L34.find_is_directory(L55[0]) and L57:find('2124089493w.cfg') then
            L54[#L54 + 1] = L57
        end;
        L56 = L34.find_next(L55[0])
    end;
    L34.find_close(L55[0])
    return L54
end;
function update_cfg()
    local L58 = L53()
    local L59 = {}
    for L60 = 1, #L58 do
        L59[L60] = L58[L60]:gsub('2124089493w.cfg', '')
    end;
    return L59
end;
local L61 = vtable_bind("vgui2.dll", "VGUI_System010", 22, "bool(__thiscall*)(void*, const char*)")
  --if L61("-insecure") then
  --  L24.set(L24.reference("MISC", "Miscellaneous", "Unlock hidden cvars"), true)
--end;
local L62 = { attack = L21.lshift(1, 0), use = L21.lshift(1, 5) }
local L63 = L16.typeof("struct { float pitch; float yaw; float roll; }")
local L64 = L16.typeof("struct { float x; float y; float z; }")
local L65 = L16.typeof([[
        struct
        {
            uintptr_t vfptr;
            int command_number;
            int tick_count;
            $ viewangles;
            $ aimdirection;
            float forwardmove;
            float sidemove;
            float upmove;
            int buttons;
            uint8_t impulse;
            int weaponselect;
            int weaponsubtype;
            int random_seed;
            short mousedx;
            short mousedy;
            bool hasbeenpredicted;
            $ headangles;
            $ headoffset;
        }
        ]], L63, L64, L63, L64)
local L66 = L16.typeof("$* (__thiscall*)(uintptr_t ecx, int nSlot, int sequence_number)", L65)
local L67 = L16.typeof([[
        struct
        {
            uintptr_t padding[8];
            $ GetUserCmd;
        }
        ]], L66)
local L68 = L16.typeof([[
        struct
        {
            $* vfptr;
        }*
        ]], L67)
local L69 = L16.cast(L68, L16.cast("uintptr_t**", L12(L16.cast("uintptr_t", L28.find_signature("client.dll", "\xB9\xCC\xCC\xCC\xCC\x8B\x40\x38\xFF\xD0\x84\xC0\x0F\x85") or error("client.dll!:input not found."))) + 1)[0])
local L70 = { reset_once = false, hitgroup_names = { [0] = "body", "head", "chest", "stomach", "left arm", "right arm", "left leg", "right leg", "neck", "?", "gear" }, fire_total_hits = 0, post_total_hits = 0, current_condition = "", mode = "back", is_defensive_running = false, banana = false, old_tick_count = 0, yaw_increment_spin = 0, tickbase_max, tickbase_diff, current_cmd, bomb_defused = false, bomb_exploded = false, pulse = 240, started = 10, smooth_idealyaw = 0, smooth_dt = 0, smooth_os = 0, smooth_pc = 0, smooth_bo = 0, current_desync = 0, fake_fakelag = 0, cur = 0, is_defusing = false, desync_rect_dist = 0, dt_os_text_anim = 0, current_cond_text_anim = 0, smooth_idealyaw_recode = 0, smooth_dt_2 = 0, smooth_stance = 0, dt_vertical_dist = 0, jumping = false, on_ground = false, rage_fired = false, last_jump_ducked = false, landing = false, waiting_scan_text = 0, hittable = false, defensive_risk = 0, smooth_defensive_bar = 0, smooth_left_arrow = 0, smooth_right_arrow = 0, smooth_up_arrow = 0, smooth_arrow_alpha = 0 }
local L71 = { cur = {}, prev = {}, pre_prev = {}, pre_pre_prev = {} }
local L72 = {}
local L73 = {}
for L74 = 1, 64 do
    L73[L74] = { stand = {}, stand_type = {}, run = {}, run_type = {}, air = {}, air_type = {}, duck = {}, duck_type = {} }
end;
local L75 = { ["user"] = "user", ["build"] = "recode" }
local L76 = L24.new_checkbox("AA", "Anti-aimbot angles", "idealyaw - " .. L22.lower(L75["user"]))
local L77 = nil;
local L78 = nil;
local L79 = nil;
local L80 = nil;
local L81 = { "anti-aim", "anti-aim 2", "visuals", "misc", "config", "debug" }
local L82 = {}
local L83 = {}
local L84 = { "global", "standing", "moving", "slow motion", "in air", "in air duck", "in duck", "in duck moving", "in fake duck", "fakelag", "manual", "freestanding", "backstab", "height", "high distance", "legit" }
local L85 = { ["lua"] = "", ["star"] = "", ["lock"] = "", ["arrows"] = "", ["pizza"] = "", ["up arrow"] = "", ["cpu"] = "", ["smilie"] = "", ["heart"] = "" }
local L86 = { le_icon = "a", tabs_names = { "", "⑵", "", "", "", "F" }, tab = {}, selected_tab = 0, selected_color = { { 20, 20, 20, 255 }, { 210, 210, 210, 255 } }, is_open = true, menu_alpha = 255, is_hovered = false, height = 68, dpi_scaling_y = { { 84, 149 }, { 100, 181 }, { 116, 213 }, { 132, 245 }, { 148, 277 } }, selected_gs_tab = false, mouse_press = false, old_mpos = { 0, 0 } }
local L87 = false;
local L88 = false;
local L89 = { ["100%"] = 68, ["125%"] = 75, ["150%"] = 85, ["175%"] = 95, ["200%"] = 105 }
local L90 = { tab = L24.new_combobox("AA", "Anti-aimbot angles", "\n", L81), ["anti-aim"] = { [0] = L24.new_combobox("AA", "Anti-aimbot angles", "type", "gamesense", "idealyaw"), [1] = L24.new_combobox("AA", "Anti-aimbot angles", "condition", L84) }, ["anti-aim 2"] = { [0] = L24.new_multiselect("AA", "Anti-aimbot angles", "add features", "other anti-aim binds", "manual anti-aim"), [1] = L24.new_hotkey("AA", "Anti-aimbot angles", "edge-yaw"), [2] = L24.new_hotkey("AA", "Anti-aimbot angles", "freestanding"), [3] = L24.new_checkbox("AA", "Anti-aimbot angles", "manual anti-aim"), [4] = L24.new_hotkey("AA", "Anti-aimbot angles", "left"), [8] = L24.new_slider("AA", "Anti-aimbot angles", "\n left angle", 0, 145, 90, true, "°", 1, {}), [5] = L24.new_hotkey("AA", "Anti-aimbot angles", "right"), [9] = L24.new_slider("AA", "Anti-aimbot angles", "\n right angle", 0, 145, 90, true, "°", 1, {}), [6] = L24.new_hotkey("AA", "Anti-aimbot angles", "forward"), [7] = L24.new_hotkey("AA", "Anti-aimbot angles", "reset") }, ["visuals"] = { [0] = L24.new_combobox("AA", "Anti-aimbot angles", "indicators", "off", "minimal (og)", "ideal yaw", "recode alpha"), [1] = L24.new_color_picker("AA", "Anti-aimbot angles", "anti-aim indicators", 200, 200, 255, 255), [6] = L24.new_multiselect("AA", "Anti-aimbot angles", "indicator extras", "animations on scope", "lowercase", "min damage", "desync", "defensive"), [3] = L24.new_combobox("AA", "Anti-aimbot angles", "indicators size", "small", "thin", "bold", "blind"), [2] = L24.new_checkbox("AA", "Anti-aimbot angles", "watermark"), [4] = L24.new_combobox("AA", "Anti-aimbot angles", "size", "small", "thin", "bold", "blind"), [7] = L24.new_checkbox("AA", "Anti-aimbot angles", "notifications size"), [5] = L24.new_combobox("AA", "Anti-aimbot angles", "\n nigga", "small", "thin", "bold", "blind"), [8] = L24.new_combobox("AA", "Anti-aimbot angles", "extended teleport prediction", "off", "box", "circle"), [9] = L24.new_checkbox("AA", "Anti-aimbot angles", "manual anti-aim"), [10] = L24.new_color_picker("AA", "Anti-aimbot angles", "manual anti-aim", 200, 200, 200, 200) }, ["misc"] = { [6] = L24.new_hotkey("AA", "Anti-aimbot angles", "extended teleport"), [7] = L24.new_hotkey("AA", "Anti-aimbot angles", "extended teleport on hit"), [8] = L24.new_combobox("AA", "Anti-aimbot angles", "extended teleport hit risk", "high", "medium", "low", "safest"), [1] = L24.new_multiselect("AA", "Anti-aimbot angles", "custom animations", "pitch on land", "fallen legs", "moonwalk", "air walk", "blind", "fake walk", "earthquake", "slide", "fake duck", "smoothing"), [2] = L24.new_multiselect("AA", "Anti-aimbot angles", "notify", "fire", "damage", "miss", "hurt", "hurt self", "config changes"), [3] = L24.new_multiselect("AA", "Anti-aimbot angles", "type \n nots", "default", "center", "console"), [4] = L24.new_checkbox("AA", "Anti-aimbot angles", "trashtalk"), [5] = L24.new_checkbox("AA", "Anti-aimbot angles", "bypass anti trashtalk") }, ["config"] = { [0] = L24.new_label("AA", "Anti-aimbot angles", "config"), [1] = L24.new_listbox("AA", "Anti-aimbot angles", "config_board", ""), [2] = L24.new_textbox("AA", "Anti-aimbot angles", "config names"), [8] = 0, [3] = 0, [4] = 0, [5] = 0, [6] = 0, [7] = 0 }, ["debug"] = { [0] = L24.new_checkbox("AA", "Anti-aimbot angles", "alternative ui"), [4] = L24.new_combobox("AA", "Anti-aimbot angles", "debug tab icon", "lua", "star", "lock", "arrows", "pizza", "up arrow", "cpu", "smilie", "heart"), [2] = L24.new_checkbox("AA", "Anti-aimbot angles", "fps optimizations"), [3] = L24.new_multiselect("AA", "Anti-aimbot angles", "disable\n optiz", "3d sky", "fog", "shadows", "blood", "decals", "bloom", "other"), [1] = L24.new_combobox("AA", "Anti-aimbot angles", "anti-aim correction", "off", "desync"), [5] = L24.new_checkbox("AA", "Anti-aimbot angles", "dynamic (ragebot)"), [6] = L24.new_hotkey("AA", "Anti-aimbot angles", "\n dynamic bind", true) } }
L24.new_label("Players", "Adjustments", "idealyawanti-aim stealer")
steal_aa_toggle = L24.new_checkbox("Players", "Adjustments", "scan anti-aim")
steal_aa_ignore = L24.new_checkbox("Players", "Adjustments", "ignore missing stances")
for L91, L92 in L10(L84) do
    L82[L91] = { [0] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("[%s - gamesense]", L92)), [1] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("pitch \n %s", L92), { "off", "default", "up", "down", "minimal", "random", "custom" }), [2] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("\n%s pitch slider", L92), -89, 89, 0, true, "°", 1, {}), [3] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("yaw base \n%s", L92), { "local view", "at targets" }), [4] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("yaw\n %s", L92), { "off", "180", "spin", "static", "180 Z", "crosshair" }), [5] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("\n%s yaw add", L92), -180, 180, 0, true, "°", 1, {}), [6] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("yaw jitter\n%s", L92), { "off", "offset", "center", "random", "skitter", "slow" }), [7] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("\n %s yaw jitter", L92), -180, 180, 0, true, "°", 1, {}), [8] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("body yaw\n %s", L92), { "off", "opposite", "jitter", "static" }), [9] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("\n%s body yaw static side", L92), -180, 180, 0, true, "°", 1, {}), [10] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("freestanding body yaw\n %s", L92)), [11] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("edge yaw\n %s", L92)), [12] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("freestanding\n %s", L92)), [13] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("roll\n %s", L92), -45, 45, 0, true, "°", 1, {}), [14] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("force defensive\n %s", L92)), [15] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("defensive pitch\n %s", L92), "off", "up", "random", "minimal", "zero"), [16] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("defensive yaw\n %s", L92), "off", "forward", "spin", "jitter", "opposite") }
    L83[L91] = { [0] = L24.new_checkbox("AA", "Anti-aimbot angles", L22.format("[%s - idealyaw] (incomplete)", L92)), [1] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("pitch\n %s w", L92), { "off", "emotion (89)", "up (-89)", "fake up (180)", "fake down (-180)", "fake zero (1080)", "fake down (-540)" }), [2] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("yaw jitter\n %s w", L92), { "off", "offset", "center", "random", "3 way", "5 way" }), [3] = L24.new_slider("AA", "Anti-aimbot angles", L22.format("\n %s yaw jitter w", L92), -180, 180, 0, true, "°", 1, {}), [4] = L24.new_combobox("AA", "Anti-aimbot angles", L22.format("body yaw\n %s w", L92), { "off", "opposite", "jitter", "static" }) }
end;
local L97 = function(L93)
    local L94 = "\n{"
    for L95, L96 in L10(L93) do
        if type(L95) == "string" then
            L94 = L94 .. "[\"" .. L95 .. "\"]" .. "="
        end;
        if type(L96) == "table" then
            L94 = L94 .. table_to_string(L96)
        elseif type(L96) == "boolean" then
            L94 = L94 .. L13(L96)
        else
            L94 = L94 .. "\"" .. L96 .. "\""
        end;
        L94 = L94 .. ",\n"
    end;
    if L94 ~= "" then
        L94 = L94:sub(1, L94:len() - 1)
    end;
    return L94 .. "}\n"
end;
local L102 = function(L98, L99)
    local L100 = {}
    for L101 in L22.gmatch(L98, "([^" .. L99 .. "]+)") do
        L100[#L100 + 1] = L22.gsub(L101, "\n", "")
    end;
    return L100
end;
local L104 = function(L103)
    if L103 == "true" or L103 == "false" then
        return L103 == "true"
    else
        return L103
    end
end;
local L106 = function(L105)
    return L23.floor(L105 + 0.5)
end;
local L110 = function(L107, L108, L109)
    return L23.max(L23.min(L107, L109), L108)
end;
local L115 = function(L111, L112, L113, L114)
    return L22.format('%02x%02x%02x%02x', L111, L112, L113, L114)
end;
local L120 = function(L116)
    local L117 = {}
    for L118, L119 in L9(L116) do
        L117[L119] = (L117[L119] or 0) + 1
    end;
    return L117
end;
local L124 = function(L121)
    local L122 = next(L121)
    for L123 in L10(L121) do
        if L121[L122] < L121[L123] then
            L122 = L123
        end
    end;
    return L122
end;
local L126 = function(L125)
    return L124(L120(L125))
end;
local L127 = { rage = { ref_doubletap = { L24.reference("RAGE", "Aimbot", "Double tap") }, ref_safepoint = L24.reference("RAGE", "Aimbot", "Force safe point"), ref_baim = { L24.reference("RAGE", "Aimbot", "Force body aim") }, ref_min_damage = { L24.reference("RAGE", "Aimbot", "Minimum damage") }, ref_min_damage_override = { L24.reference("RAGE", "Aimbot", "Minimum damage override") }, other = { ref_fakeduck = L24.reference("RAGE", "Other", "Duck peek assist") } }, anti_aim = { anti_aimbot_angles = { ref_aa_enabled = L24.reference("AA", "Anti-aimbot angles", "Enabled"), ref_pitch = { L24.reference("AA", "Anti-aimbot angles", "Pitch") }, ref_yaw = { L24.reference("AA", "Anti-aimbot angles", "Yaw") }, ref_yaw_base = L24.reference("AA", "Anti-aimbot angles", "Yaw base"), ref_body_yaw = { L24.reference("AA", "Anti-aimbot angles", "Body yaw") }, ref_yaw_jitter = { L24.reference("AA", "Anti-aimbot angles", "Yaw jitter") }, ref_freestand_body = L24.reference("AA", "Anti-aimbot angles", "Freestanding body yaw"), ref_edge_yaw = L24.reference("AA", "Anti-aimbot angles", "Edge yaw"), ref_freestand = { L24.reference("AA", "Anti-aimbot angles", "Freestanding") }, ref_roll = L24.reference("AA", "Anti-aimbot angles", "Roll") }, fakelag = {}, other = { ref_slowmotion = { L24.reference("AA", "Other", "Slow motion") }, ref_onshotantiaim = { L24.reference("AA", "Other", "On shot anti-aim") } } }, misc = { settings = { ref_dpiscale = L24.reference("MISC", "Settings", "DPI scale"), ref_menukey = L24.reference("MISC", "Settings", "Menu key"), ref_nadetoss = L24.reference("MISC", "Settings", "Faster grenade toss") }, movement = { ref_bhop = L24.reference('MISC', 'Movement', 'Bunny hop') } }, plist = { players = L24.reference("Players", "Players", "Player list"), force_yaw = L24.reference("Players", "Adjustments", "Force body yaw"), force_yaw_value = L24.reference("Players", "Adjustments", "Force body yaw value"), force_body = L24.reference("Players", "Adjustments", "Force body yaw"), force_body_value = L24.reference("Players", "Adjustments", "Force body yaw value"), reset = L24.reference("Players", "Players", "Reset all") } }
local L132 = function(L128, L129)
    local L130 = false;
    for L131 = 1, #L128 do
        if L128[L131] == L129 then
            L130 = true;
            break
        end
    end;
    return L130
end;
local L136 = function(L133, L134, L135)
    return L133 + (L134 - L133) * L135
end;
local L138 = function(L137)
    while L137 > 180 do
        L137 = L137 - 360
    end;
    while L137 < -180 do
        L137 = L137 + 360
    end;
    return L137
end;
function calculate_angle(L139, L140)
    local L141 = L140 - L139;
    local L142 = L23.atan(L141.y / L141.x)
    L142 = L138(L142 * 180 / L23.pi)
    if L141.x >= 0 then
        L142 = L138(L142 + 180)
    end;
    return L142
end;
local L145 = function(L143)
    local L144 = L27.get_prop(L143, "m_bIsScoped")
    if L144 == 1 then
        return true
    end;
    return false
end;
local L146 = {}
local L147 = {}
L24.set_callback(steal_aa_ignore, function()
    if L24.get(steal_aa_ignore) then
        L146[L24.get(L127.plist.players)] = true
    else
        if L146[L24.get(L127.plist.players)] then
            L146[L24.get(L127.plist.players)] = nil
        end
    end
end)
L24.set_callback(L127.plist.players, function()
    L24.set(steal_aa_ignore, L146[L24.get(L127.plist.players)] ~= nil)
end)
L24.set_callback(L127.plist.reset, function()
    L146 = {}
    L24.set(steal_aa_ignore, false)
end)
L24.set_callback(steal_aa_toggle, function()
    if L24.get(steal_aa_toggle) then
        L147[L24.get(L127.plist.players)] = true
    else
        if L147[L24.get(L127.plist.players)] then
            L147[L24.get(L127.plist.players)] = nil
        end
    end
end)
L24.set_callback(L127.plist.players, function()
    L24.set(steal_aa_toggle, L147[L24.get(L127.plist.players)] ~= nil)
end)
L24.set_callback(L127.plist.reset, function()
    L147 = {}
    L24.set(steal_aa_toggle, false)
end)
local L148 = function()
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_aa_enabled, false)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[1], "Off")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[2], 0)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[1], "Off")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], 0)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_base, "Local view")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[1], "Off")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[2], 0)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1], "Off")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[2], 0)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand_body, false)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_edge_yaw, false)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand[1], false)
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand[2], "Always on")
    L24.set(L127.anti_aim.anti_aimbot_angles.ref_roll, 0)
end;
local L154 = function(L149)
    for L150, L151 in L10(L127.anti_aim.anti_aimbot_angles) do
        if type(L151) ~= "table" then
            L24.set_visible(L151, not L149)
            if not L149 and L24.get(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[1]) == "Off" then
                L24.set_visible(L127.anti_aim.anti_aimbot_angles.ref_freestand_body, false)
            end
        else
            for L152, L153 in L9(L151) do
                L24.set_visible(L153, not L149)
                if not L149 and L24.get(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[1]) == "Opposite" then
                    L24.set_visible(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[2], false)
                end;
                if not L149 and L24.get(L151[1]) == "Off" and L150 ~= "ref_pitch" then
                    L24.set_visible(L151[2], false)
                    if L24.get(L127.anti_aim.anti_aimbot_angles.ref_yaw[1]) == "Off" then
                        L24.set_visible(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1], false)
                    end
                end;
                if not L149 and L24.get(L127.anti_aim.anti_aimbot_angles.ref_pitch[1]) ~= "Custom" then
                    L24.set_visible(L127.anti_aim.anti_aimbot_angles.ref_pitch[2], false)
                end
            end
        end
    end
end;
local L155, L156 = L28.screen_size()
local L157 = { x = L20.read("x_82hdnujdsgfu") or L155 - L155 + 10, y = L20.read("y_ajshdahjdjhn") or L156 - L156 + 550, w = L20.read("w_akjdfsahsdff") or 100, h = L20.read("h_pi2jpoaojkfs") or 100, dragging = false }
local function L158(L159, L160, L161, L162)
    local L163, L164 = L24.mouse_position()
    return L163 >= L159 and L163 <= L159 + L161 and L164 >= L160 and L164 <= L160 + L162
end;
function watermark(L165, L166)
    if not L24.get(L90["visuals"][2]) then
        return
    end;
    local L167 = ""
    local L168 = "idealyaw [" .. L22.upper(L75["build"]) .. "]" .. " | " .. L22.upper(L75["user"]) .. " | " .. L23.floor(L28.latency() * 1000) .. "MS"
    if L166 == "small" then
        L167 = "-"
        L168 = "idealyaw   [" .. L22.upper(L75["build"]) .. "]" .. "   |   " .. L22.upper(L75["user"]) .. "   |   " .. L23.floor(L28.latency() * 1000) .. "MS"
    elseif L166 == "thin" then
        L167 = ""
    elseif L166 == "bold" then
        L167 = "b"
    elseif L166 == "blind" then
        L167 = "+"
    end;
    local L169, L170 = L28.screen_size()
    local L171 = { L24.mouse_position() }
    local L172 = L28.key_state(0x01)
    local L173 = { L25.measure_text(L167, L168) }
    if L24.is_menu_open() then
        if L157.dragging and not L172 then
            L157.dragging = false
        end;
        if L157.dragging and L172 then
            L157.x = L171[1] - L157.drag_x;
            L157.y = L171[2] - L157.drag_y
        end;
        if L158(L157.x, L157.y, L157.w + L173[1], L157.h + L173[2]) and L172 then
            L157.dragging = true;
            L157.drag_x = L171[1] - L157.x;
            L157.drag_y = L171[2] - L157.y
        end
    end;
    if L157.x + L173[1] > L169 then
        L157.x = L157.x - 5
    elseif L157.x + 20 < 0 then
        L157.x = L157.x + 5
    end;
    if L157.y + L173[2] > L170 then
        L157.y = L157.y - 10
    elseif L157.y + L173[2] < 0 then
        L157.y = L157.y + 10
    end;
    local L174 = {}
    L25.gradient(L157.x, L157.y + L173[2] + 8, L173[1] / 1.5, 1, 0, 0, 0, 0, 220, 220, 220, 220, 255, true)
    L25.gradient(L157.x + L173[1] / 1.5, L157.y + L173[2] + 8, L173[1] / 1.5, 1, 220, 220, 220, 255, 0, 0, 0, 0, true)
    L25.gradient(L157.x, L157.y, L173[1] / 1.5, L173[2] + 7, 12, 12, 12, 0, 12, 12, 12, 75, true)
    L25.gradient(L157.x + L173[1] / 1.5, L157.y, L173[1] / 1.5, L173[2] + 7, 12, 12, 12, 75, 12, 12, 12, 0, true)
    L25.text(L157.x + 18, L157.y + 5, 255, 255, 255, 220, L167, 0, L168)
    if not L27.is_alive(L165) then
        return
    end;
    table.insert(L174, { text = "- CONDITION: " .. L22.upper(L70.current_condition), r = 240, g = 240, b = 240, a = 220 })
    table.insert(L174, { text = "- TARGET: " .. L22.upper(L28.current_threat() == nil and "?" or L22.sub(L27.get_player_name(L28.current_threat()), 0, 12)), r = 240, g = 240, b = 240, a = 220 })
    table.insert(L174, { text = "- EXPLOIT CHARGE: " .. (L3.get_double_tap() == false and "0" or "1"), r = 240, g = 240, b = 240, a = 220 })
    table.insert(L174, { text = "- DESYNC: " .. L22.upper(L23.abs(L70.current_desync)) .. "*", r = 240, g = 240, b = 240, a = 220 })
    for L175, L176 in L10(L174) do
        text_size2 = { L25.measure_text(L167, L176.text) }
        L25.text(L157.x + 18, 10 + L157.y + text_size2[2] * L175, L176.r, L176.g, L176.b, L176.a, L167, 0, L176.text)
    end
end;
function draw_glow(L177, L178, L179, L180, L181, L182)
    L25.rectangle(L177, L178, L179, L180, L181[1], L181[2], L181[3], L181[4])
    local L183 = L181[1] * L182;
    local L184 = L181[2] * L182;
    local L185 = L181[3] * L182;
    for L186 = 1, L182 do
        local L187 = L181[4] * L186 / L182;
        local L188 = L179 + L186 * 2;
        local L189 = L180 + L186 * 2;
        local L190 = L177 - L186;
        local L191 = L178 - L186;
        L25.rectangle(L190, L191, L188, L189, L183, L184, L185, L187)
    end
end;
local L197 = function(L192, L193, L194, L195, L196)
    if not L132(L24.get(L90["visuals"][6]), "desync") then
        return
    end;
    dsy_rect = { 255, 255, 255, 255 }
    L196 = L196 + 5;
    if L145(L192) and L132(L24.get(L90["visuals"][6]), "animations on scope") then
        L70.desync_rect_dist = L136(L70.desync_rect_dist, 21 + 2, L26.frametime() * 15)
    elseif not L132(L24.get(L90["visuals"][6]), "animations on scope") and L24.get(L90["visuals"][0]) == "recode alpha" then
        L70.desync_rect_dist = 21 + 2
    else
        L70.desync_rect_dist = L136(L70.desync_rect_dist, 0, L26.frametime() * 10)
    end;
    L25.rectangle(L193 - 21 + L106(L70.desync_rect_dist), L194 + L196, 21 * 2, 4, 15, 15, 15, 255)
    L25.rectangle(L193 - (21 - 1) + L106(L70.desync_rect_dist), L194 + L196 + 1, L110(L23.abs(L70.current_desync) / 58 * (21 * 2 - 2), 0, 21 * 2 - 2), 2, dsy_rect[1], dsy_rect[2], dsy_rect[3], dsy_rect[4])
end;
local L205 = function(L198, L199, L200)
    if not L24.get(L90["visuals"][9]) or not L24.get(L90["anti-aim 2"][3]) then
        return
    end;
    L70.smooth_left_arrow = L145(L198) and L136(L70.smooth_left_arrow, 80, L26.frametime() * 15) or L136(L70.smooth_left_arrow, 60, L26.frametime() * 15)
    L70.smooth_right_arrow = L145(L198) and L136(L70.smooth_right_arrow, 80, L26.frametime() * 15) or L136(L70.smooth_right_arrow, 60, L26.frametime() * 15)
    L70.smooth_up_arrow = L145(L198) and L136(L70.smooth_up_arrow, 80, L26.frametime() * 15) or L136(L70.smooth_up_arrow, 60, L26.frametime() * 15)
    local L201 = { ["left"] = { indicator = "", x_pos = -L70.smooth_left_arrow, y_pos = -5 }, ["right"] = { indicator = "", x_pos = L70.smooth_left_arrow, y_pos = -5 }, ["forward"] = { indicator = "", x_pos = 0, y_pos = -L70.smooth_up_arrow } }
    local L202 = { L24.get(L90["visuals"][10]) }
    L70.smooth_arrow_alpha = L145(L198) and L136(L70.smooth_arrow_alpha, L110(L202[4] - 100, 0, 235), L26.frametime() * 15) or L136(L70.smooth_arrow_alpha, L202[4], L26.frametime() * 15)
    for L203, L204 in L10(L201) do
        if L203 == L70.mode then
            L25.text(L199 + L23.ceil(L204.x_pos), L200 + L23.ceil(L204.y_pos), L202[1], L202[2], L202[3], L70.smooth_arrow_alpha, "c+", 0, L204.indicator)
        end
    end
end;
local L213 = function(L206, L207, L208)
    if not L132(L24.get(L90["visuals"][6]), "defensive") then
        return
    end;
    if L70.tickbase_diff ~= nil and L70.tickbase_diff <= -1 and L70.tickbase_diff >= -14 then
        defensive_size_x, defensive_size_y = L25.measure_text("c", "- defensive -")
        defensive_size_x = defensive_size_x + 15;
        L25.rectangle(L207 - defensive_size_x / 2, L208 / 3 + defensive_size_y - 2, defensive_size_x, 4, 15, 15, 15, 150)
        local L209 = L70.tickbase_diff;
        local L210 = L23.abs(-L209 - 15)
        local L211 = L210;
        if L210 == L211 and L210 > 1 then
            L211 = L211 - 1
        end;
        L70.smooth_defensive_bar = L136(L70.smooth_defensive_bar, L211, L26.frametime() * 50)
        local L212 = L136(75, 200, (L70.smooth_defensive_bar - 1) / 12)
        L25.text(L207, L208 / 3, 255, 255, 255, L212, "c", 0, "- defensive -")
        L25.rectangle(L207 + 1 - defensive_size_x / 2, L208 / 3 + 10, L110(L70.smooth_defensive_bar / 12 * defensive_size_x, 0, defensive_size_x) - 2, 2, 200, 200, 200, L212)
    else
        L70.smooth_defensive_bar = 0.5
    end
end;
local L226 = function(L214, L215, L216)
    local L217 = L26.tickinterval()
    local L218 = cvar.sv_gravity:get_float() * L217;
    local L219 = cvar.sv_jump_impulse:get_float() * L217;
    local L220 = { L215[1], L215[2], L215[3] }
    local L221 = { L27.get_prop(L214, 'm_vecVelocity') }
    local L222 = L221[3] > 0 and -L218 or L219;
    for L223 = 1, L216 do
        local L224 = { L220[1], L220[2], L220[3] }
        L220[1] = L220[1] + L221[1] * L217;
        L220[2] = L220[2] + L221[2] * L217;
        L220[3] = L220[3] + (L221[3] + L222) * L217;
        local L225 = L28.trace_line(L224[1], L224[2], L224[3], L220[1], L220[2], L220[3])
        if L225.fraction <= 0.99 then
            return L224
        end
    end;
    return L220
end;
local L229 = function(L227, L228)
    return { L227[1] + L228[1], L227[2] + L228[2], L227[3] + L228[3] }
end;
local L240 = function(L230, L231)
    local L232 = L26.tickinterval()
    local L233 = cvar.sv_gravity:get_float() * L232;
    local L234 = cvar.sv_jump_impulse:get_float() * L232;
    local L235 = { L27.get_origin(L230) }
    local L236 = { L27.get_origin(L230) }
    local L237 = { L27.get_prop(L230, 'm_vecVelocity') }
    local L238 = L237[3] > 0 and -L233 or L234;
    for L239 = 1, L231 do
        L236 = L235;
        L235 = { L235[1] + L237[1] * L232, L235[2] + L237[2] * L232, L235[3] + (L237[3] + L238) * L232 }
    end;
    return L235
end;
local L251 = function(L241, L242, L243)
    local L244 = L229({ L27.get_prop(L241, 'm_vecMins') }, L242)
    local L245 = L229({ L27.get_prop(L241, 'm_vecMaxs') }, L242)
    local L246 = { { L244[1], L244[2], L244[3] }, { L244[1], L245[2], L244[3] }, { L245[1], L245[2], L244[3] }, { L245[1], L244[2], L244[3] }, { L244[1], L244[2], L245[3] }, { L244[1], L245[2], L245[3] }, { L245[1], L245[2], L245[3] }, { L245[1], L244[2], L245[3] } }
    local L247 = { { 0, 1 }, { 1, 2 }, { 2, 3 }, { 3, 0 }, { 5, 6 }, { 6, 7 }, { 1, 4 }, { 4, 8 }, { 0, 4 }, { 1, 5 }, { 2, 6 }, { 3, 7 }, { 5, 8 }, { 7, 8 }, { 3, 4 } }
    for L248 = 1, #L247 do
        if L246[L247[L248][1]] ~= nil and L246[L247[L248][2]] ~= nil then
            local L249 = { L25.world_to_screen(L246[L247[L248][1]][1], L246[L247[L248][1]][2], L246[L247[L248][1]][3]) }
            local L250 = { L25.world_to_screen(L246[L247[L248][2]][1], L246[L247[L248][2]][2], L246[L247[L248][2]][3]) }
            L25.line(L249[1], L249[2], L250[1], L250[2], 255, 255, 255, 255)
        end
    end
end;
local function L252(L253, L254, L255, L256, L257, L258, L259, L260, L261)
    local L262 = L261 or 3;
    local L263, L264;
    for L265 = 0, 360, L262 do
        local L266 = L23.rad(L265)
        local L267, L268, L269 = L256 * L23.cos(L266) + L253, L256 * L23.sin(L266) + L254, L255;
        local L270, L271 = L25.world_to_screen(L267, L268, L269)
        if L270 ~= nil and L263 ~= nil then
            L25.line(L270, L271, L263, L264, L257, L258, L259, L260)
        end;
        L263, L264 = L270, L271
    end
end;
local function L272(L273, L274, L275, L276, L277, L278, L279, L280, L281)
    local L282 = L281 or 3;
    local L283 = {}
    for L284 = 0, 360, L282 do
        local L285 = L23.rad(L284)
        local L286, L287, L288 = L276 * L23.cos(L285) + L273, L276 * L23.sin(L285) + L274, L275;
        table.insert(L283, { L286, L287, L288 })
    end;
    for L289 = 1, #L283 - 2 do
        local L290, L291, L292 = L283[1], L283[L289 + 1], L283[L289 + 2]
        local L293, L294 = L25.world_to_screen(L290[1], L290[2], L290[3])
        local L295, L296 = L25.world_to_screen(L291[1], L291[2], L291[3])
        local L297, L298 = L25.world_to_screen(L292[1], L292[2], L292[3])
        if L293 and L295 and L297 then
            L25.triangle(L293, L294, L295, L296, L297, L298, L277, L278, L279, L280)
        end
    end
end;
local function L299(L300, L301, L302, L303, L304, L305, L306, L307, L308, L309)
    local L310 = L308 or 3;
    local L311 = L309 or 5;
    local L312 = L307 / L311;
    local L313 = L307;
    for L314 = 1, L311 do
        L252(L300, L301, L302, L303 + L314, L304, L305, L306, L313, L310)
        L313 = L313 - L312
    end
end;
local L316 = function(L315)
    if L24.get(L127.anti_aim.other.ref_onshotantiaim[1]) and L24.get(L127.anti_aim.other.ref_onshotantiaim[2]) or not (L24.get(L90["misc"][6]) or L24.get(L90["misc"][7]) and L70.hittable) or L70.tickbase_diff == nil or L70.tickbase_diff > 0 then
        return
    end;
    if not L24.get(L127.rage.ref_doubletap[1]) and not L24.get(L127.rage.ref_doubletap[2]) then
        return
    end;
    predicted_pos = L240(L315, 14)
    if L24.get(L90["visuals"][8]) == "circle" then
        L299(predicted_pos[1], predicted_pos[2], predicted_pos[3], 6, 255, 255, 255, 255, 3, 10)
        L272(predicted_pos[1], predicted_pos[2], predicted_pos[3], 7, 255, 255, 255, 150, 3)
    elseif L24.get(L90["visuals"][8]) == "box" then
        L251(L315, predicted_pos, true)
    end
end;
local L317 = { main = { 0, 1, 6, 5, 4, 3, 2 }, left_arm = { 14, 18, 17, 1 }, right_arm = { 13, 16, 15, 1 }, left_leg = { 12, 10, 8, 2 }, right_leg = { 11, 9, 7, 2 } }
local L330 = function(L318, L319, L320)
    local L321 = L26.tickinterval()
    local L322 = cvar.sv_gravity:get_float() * L321;
    local L323 = cvar.sv_jump_impulse:get_float() * L321;
    local L324, L325 = L319, L319;
    local L326 = { L27.get_prop(L318, 'm_vecVelocity') }
    local L327 = L326[3] > 0 and -L322 or L323;
    for L328 = 1, L320 do
        L325 = L324;
        L324 = { L324[1] + L326[1] * L321, L324[2] + L326[2] * L321, L324[3] + (L326[3] + L327) * L321 }
        local L329 = L28.trace_line(-1, L325[1], L325[2], L325[3], L324[1], L324[2], L324[3])
    end;
    return L324
end;
local L350 = function(L331)
    for L332, L333 in L10(L317) do
        for L334, L335 in L10(L333) do
            if L334 ~= #L333 then
                local L336 = {}
                for L337 = 0, 18 do
                    local L338 = { L27.hitbox_position(L331, L337) }
                    local L339 = L338;
                    L336[L337] = { x = L339[1], y = L339[2], z = L339[3] }
                end;
                local L340, L341, L342 = L336[L333[L334]].x, L336[L333[L334]].y, L336[L333[L334]].z;
                local L343, L344 = L25.world_to_screen(L340, L341, L342)
                local L345, L346, L347 = L336[L333[L334 + 1]].x, L336[L333[L334 + 1]].y, L336[L333[L334 + 1]].z;
                local L348, L349 = L25.world_to_screen(L345, L346, L347)
                L25.line(L343, L344, L348, L349, 255, 255, 255, 255)
            end
        end
    end
end;
local function L351(L352, L353, L354)
    local L355 = L22.len(L353)
    if L352 < L355 then
        L352 = L352 + 1 * L26.frametime() * L354
    else
        L352 = L355
    end;
    local L356 = L23.floor(L352)
    local L357 = L22.sub(L353, 1, L356)
    return L352, L357
end;
local L358 = ""
local L401 = function(L359, L360, L361, L362, L363)
    if not L360 or not L27.is_alive(L361) then
        return
    end;
    L316(L361)
    local L364 = {}
    local L365, L366, L367, L368 = L24.get(L90["visuals"][1])
    local L369, L370 = L362[1] / 2, L362[2] / 2;
    local L371 = ""
    L213(L361, L369, L370)
    L205(L361, L369, L370)
    if L363 == "small" then
        L371 = "-"
    elseif L363 == "thin" then
        L371 = ""
    elseif L363 == "bold" then
        L371 = "b"
    elseif L363 == "blind" then
        L371 = "+"
    end;
    if L24.get(L90["visuals"][0]) ~= "recode alpha" then
        L70.smooth_idealyaw_recode = 0;
        L70.smooth_dt_2 = 0;
        L70.smooth_stance = 0;
        L70.dt_os_text_anim = 0;
        L70.current_cond_text_anim = 0
    end;
    if L24.get(L360) == "minimal (og)" then
        local L372 = "SP BAIM FS"
        local L373 = "SP"
        local L374 = " BAIM"
        local L375 = " FS"
        local L376 = "idealyaw"
        local L377 = "DT"
        local L378 = "OS"
        local L379 = L22.upper(L70.current_condition)
        if L371 == "-" then
            L373 = "SP"
            L374 = "  BAIM"
            L375 = "  FS"
            L372 = "SP  BAIM  FS"
        end;
        if L132(L24.get(L90["visuals"][6]), "lowercase") then
            L376 = L22.lower(L376)
            L377 = L22.lower(L377)
            L378 = L22.lower(L378)
            L372 = L22.lower(L372)
            L373 = L22.lower(L373)
            L374 = L22.lower(L374)
            L375 = L22.lower(L375)
            L379 = L22.lower(L379)
        end;
        local L380 = { L25.measure_text(L371, L376) }
        L70.smooth_idealyaw = L145(L361) and L136(L70.smooth_idealyaw, -2, L26.frametime() * 15) or L136(L70.smooth_idealyaw, L25.measure_text(L371, L376) / 2, L26.frametime() * 15)
        table.insert(L364, { text = L376, r = 210, g = 210, b = 210, a = 255, size = L23.ceil(L70.smooth_idealyaw) })
        L70.smooth_pc = L145(L361) and L136(L70.smooth_pc, -2, L26.frametime() * 15) or L136(L70.smooth_pc, L25.measure_text(L371, L23.abs(L70.current_desync) .. "%") / 2, L26.frametime() * 15)
        table.insert(L364, { text = L23.abs(L70.current_desync) .. "%", r = 210, g = 210, b = 210, a = 255, size = L23.ceil(L70.smooth_pc) })
        L70.smooth_dt = L145(L361) and L136(L70.smooth_dt, -2, L26.frametime() * 15) or L136(L70.smooth_dt, L25.measure_text(L371, L378) / 2, L26.frametime() * 15)
        if L24.get(L127.rage.ref_doubletap[1]) and L24.get(L127.rage.ref_doubletap[2]) then
            local L381 = L3.get_double_tap() or L70.tickbase_diff ~= 1;
            table.insert(L364, { text = L377, r = 210, g = 210, b = 210, a = L381 and 255 or 100, size = L23.ceil(L70.smooth_dt) })
            L70.dt_vertical_dist = L136(L70.dt_vertical_dist, 10, L26.frametime() * 20)
        else
            L70.dt_vertical_dist = L136(L70.dt_vertical_dist, 0, L26.frametime() * 20)
        end;
        L70.smooth_os = L145(L361) and L136(L70.smooth_os, -2, L26.frametime() * 15) or L136(L70.smooth_os, L25.measure_text(L371, L378) / 2, L26.frametime() * 15)
        if L24.get(L127.anti_aim.other.ref_onshotantiaim[1]) and L24.get(L127.anti_aim.other.ref_onshotantiaim[2]) then
            local L382 = L24.get(L127.rage.ref_doubletap[1]) and L24.get(L127.rage.ref_doubletap[2])
            table.insert(L364, { text = L378, r = 210, g = 210, b = 210, a = not L382 and 255 or L23.max(L70.pulse, 100), size = L23.ceil(L70.smooth_os) })
        end;
        L70.smooth_bo = L145(L361) and L136(L70.smooth_bo, -2, L26.frametime() * 15) or L136(L70.smooth_bo, L25.measure_text(L371, L372) / 2, L26.frametime() * 15)
        table.insert(L364, { text = ("\a%s" .. L373 .. "\a%s" .. L374 .. "\a%s" .. L375):format(L22.format("%02X%02X%02X%02X", L365, L366, L367, L24.get(L127.rage.ref_safepoint) and 210 or 100), L22.format("%02X%02X%02X%02X", L365, L366, L367, L24.get(L127.rage.ref_baim[1]) and 210 or 100), L22.format("%02X%02X%02X%02X", L365, L366, L367, L24.get(L127.anti_aim.anti_aimbot_angles.ref_freestand[1]) and L24.get(L127.anti_aim.anti_aimbot_angles.ref_freestand[2]) and 210 or 100)), r = 210, g = 210, b = 210, a = 255, size = L23.ceil(L70.smooth_bo) })
        for L383, L384 in L10(L364) do
            L25.text(L369 + (L132(L24.get(L90["visuals"][6]), "animations on scope") == true and -L384.size or -(L25.measure_text(L371, L384.text) / 2)), 10 + L370 + L380[2] * L383, L384.r, L384.g, L384.b, L384.a, L371, 0, L384.text)
        end;
        local L385 = { L25.measure_text(L371, L376) }
        L197(L361, L369, L370, L385[1], L385[2])
    else
        L70.smooth_idealyaw = 0;
        L70.smooth_dt = 0;
        L70.smooth_os = 0;
        L70.smooth_pc = 0;
        L70.smooth_bo = 0;
-- В функции L401 (рендеринг индикаторов) находим блок для "ideal yaw" и изменяем его:
if L24.get(L360) == "ideal yaw" then
    local text = "IDEAL YAW"
    local text_color = {255, 165, 0} -- оранжевый как оригинальный DYNAMIC
    
-- Проверяем условия для изменения текста и цвета
if L70.current_condition == "manual" then
    text = "FAKE YAW"
    text_color = {191, 159, 255} -- фиолетовый как DYNAMIC
elseif L70.current_condition == "freestanding" then
    text = "FREESTAND"
    text_color = {191, 159, 255} -- фиолетовый как DYNAMIC
elseif L70.current_condition == "legit" and client.key_state(0x45) then
    text = "E-PEEK"
    text_color = {191, 159, 255} -- тоже фиолетовый как DYNAMIC
end

    
    local mode_text = "DYNAMIC"
    local mode_color = {191, 159, 255}
    
    local yaw_mode = L24.get(L127.anti_aim.anti_aimbot_angles.ref_yaw[1])
    local jitter_mode = L24.get(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1])
    
    local static_conditions = {
        ["manual"] = true,
        ["legit"] = true
    }
    
    if static_conditions[L70.current_condition] or (yaw_mode == "Static" or yaw_mode == "Off") and jitter_mode == "Off" then
        mode_text = "DEFAULT"
        mode_color = {255, 0, 0}
    end
    

    table.insert(L364, { 
        text = text, 
        r = text_color[1], 
        g = text_color[2], 
        b = text_color[3], 
        a = 255,  
        size = L25.measure_text("", text) / 2 - 31    })
    
    table.insert(L364, { 
        text = mode_text, 
        r = mode_color[1], 
        g = mode_color[2], 
        b = mode_color[3], 
        a = 255,  
        size = L25.measure_text("", mode_text) / 2 - 26
    })

    if L24.get(L127.rage.ref_doubletap[2]) then
        local dt_recharged = L3.get_double_tap()
        local dt_color = dt_recharged and {0, 255, 0} or {255, 0, 0} -- зелёный если заряжен, красный если нет

        table.insert(L364, {
            text = "DT",
            r = dt_color[1],
            g = dt_color[2],
            b = dt_color[3],
            a = 255,
            size = L25.measure_text(L371, "DT") / 2 - 11
        })
    end

    if L24.get(L127.anti_aim.other.ref_onshotantiaim[1]) and L24.get(L127.anti_aim.other.ref_onshotantiaim[2]) then
        table.insert(L364, { 
            text = "HIDE", 
            r = 0, 
            g = 255, 
            b = 0, 
            a = 255,  
            size = L25.measure_text("", "HIDE") / 2 - 16
        })
    end

-- фиксированная отрисовка всех индикаторов по центру экрана
for index, entry in ipairs(L364) do
    L25.text(L369 +5, 10 + L370 + 12 * index, entry.r, entry.g, entry.b, entry.a, "", "c", entry.text)
end
        elseif L24.get(L360) == "recode alpha" then
            local L389 = ("idealyaw\a%s RECODE"):format(L22.format("%02X%02X%02X%02X", L365, L366, L367, L23.max(L368, 100)))
            local L390 = "DT"
            local L391 = "ON SHOT"
            local L392 = { L25.measure_text(L371, L389) }
            local L393 = L22.upper(L70.current_condition)
            if L70.mode == "left" then
                L393 = "MANUAL LEFT"
            elseif L70.mode == "right" then
                L393 = "MANUAL RIGHT"
            elseif L70.mode == "forward" then
                L393 = "MANUAL FORWARD"
            end;
            if L132(L24.get(L90["visuals"][6]), "lowercase") then
                L389 = L22.lower(L389)
                L390 = L22.lower(L390)
                L391 = L22.lower(L391)
                L393 = L22.lower(L393)
            end;
            local L394 = L3.get_double_tap() or L70.tickbase_diff ~= 1;
            local L395 = L24.get(L127.anti_aim.other.ref_onshotantiaim[1]) and L24.get(L127.anti_aim.other.ref_onshotantiaim[2])
            local L396 = L24.get(L127.rage.ref_doubletap[1]) and L24.get(L127.rage.ref_doubletap[2])
            local L397 = ""
            if L396 then
                L397 = L390
            elseif L395 then
                L397 = L391
            end;
            L70.dt_os_text_anim, ayo = L351(L70.dt_os_text_anim, L397, 50)
            L70.current_cond_text_anim, ayo2 = L351(L70.current_cond_text_anim, L393, 25)
            if L358 ~= L393 then
                if #L358 <= #L393 then
                    L70.current_cond_text_anim = #L358
                end;
                L358 = L393
            end;
            idealyaw_recode_text_size = { L25.measure_text(L371, L389) }
            L70.smooth_idealyaw_recode = L145(L361) and L136(L70.smooth_idealyaw_recode, -2, L26.frametime() * 15) or L136(L70.smooth_idealyaw_recode, idealyaw_recode_text_size[1] / 2, L26.frametime() * 15)
            table.insert(L364, { text = L389, r = 240, g = 240, b = 240, a = 255, size = L23.floor(L70.smooth_idealyaw_recode), txt_measure = { L25.measure_text(L371, L389) } })
            L70.smooth_dt_2 = L145(L361) and L136(L70.smooth_dt_2, -2, L26.frametime() * 15) or L136(L70.smooth_dt_2, L25.measure_text(L371, L397) / 2, L26.frametime() * 15)
            if L396 or L395 then
                table.insert(L364, { text = ayo, r = L396 and (L394 and 0 or 255) or 135, g = L396 and (L394 and 255 or 0) or 206, b = L396 and 0 or 250, a = 255, size = L23.floor(L70.smooth_dt_2), txt_measure = { L25.measure_text(L371, ayo) } })
            else
                L70.dt_os_text_anim = 0
            end;
            ayo2 = "'  " .. ayo2 .. "  '"
            L70.smooth_stance = L145(L361) and L136(L70.smooth_stance, -2, L26.frametime() * 15) or L136(L70.smooth_stance, L25.measure_text(L371, ayo2) / 2, L26.frametime() * 15)
            table.insert(L364, { text = ayo2, r = 240, g = 240, b = 240, a = 255, size = L23.floor(L70.smooth_stance), txt_measure = { L25.measure_text(L371, ayo2) } })
            for L398, L399 in L10(L364) do
                L25.text(L369 + (L132(L24.get(L90["visuals"][6]), "animations on scope") == true and -L399.size or 0), 10 + L370 + L392[2] * L398, L399.r, L399.g, L399.b, L399.a, L371, 0, L399.text)
            end;
            local L400 = { L25.measure_text(L371, L389) }
            L197(L361, L369, L370, L400[1], L400[2])
        end
    end
end;
gamesense_outer = function(L402, L403, L404, L405, L406, L407)
    L407 = L407 or false;
    if not L407 then
        L25.rectangle(L402, L403 - (L405 + 3), L404, 1, 12, 12, 12, L406)
        L25.rectangle(L402 + 2, L403 - (L405 + 2), L404 - 4, 5, 60, 60, 60, L406)
        L25.rectangle(L402 + 2, L403 - (L405 + 1), L404 - 4, 3, 40, 40, 40, L406)
        L25.rectangle(L402, L403 - (L405 + 3), 1, L405 + 3, 12, 12, 12, L406)
        L25.rectangle(L402 + 1, L403 - (L405 + 2), 4, L405 + 2, 60, 60, 60, L406)
        L25.rectangle(L402 + 2, L403 - (L405 + 1), 3, L405 + 1, 40, 40, 40, L406)
        L25.rectangle(L402 + 5, L403 - (L405 - 2), 1, L405 - 2, 60, 60, 60, L406)
        L25.rectangle(L402 + L404 - 1, L403 - (L405 + 3), 1, L405 + 3, 12, 12, 12, L406)
        L25.rectangle(L402 + L404 - 3, L403 - (L405 + 2), 2, L405 + 2, 60, 60, 60, L406)
        L25.rectangle(L402 + L404 - 5, L403 - (L405 + 1), 3, L405 + 1, 40, 40, 40, L406)
        L25.rectangle(L402 + L404 - 6, L403 - (L405 - 2), 1, L405 - 2, 60, 60, 60, L406)
    else
        L25.rectangle(L402 - L405 / 2 - 4, L403 - 47, L405 + 9, L404 + 9, 12, 12, 12, L406)
        L25.rectangle(L402 - L405 / 2 - 10, L403 - 53, L405 + 20, 1, 12, 12, 12, L406)
        L25.rectangle(L402 - L405 / 2 - 9, L403 - 52, L405 + 18, 1, 60, 60, 60, L406)
        L25.rectangle(L402 - L405 / 2 - 8, L403 - 51, L405 + 17, 3, 40, 40, 40, L406)
        L25.rectangle(L402 - L405 / 2 - 5, L403 - 48, L405 + 10, 1, 60, 60, 60, L406)
        L25.rectangle(L402 - L405 / 2 - 10, L403 - 53, 1, L404 + 19, 12, 12, 12, L406)
        L25.rectangle(L402 - L405 / 2 - 9, L403 - 51, 1, L404 + 18, 60, 60, 60, L406)
        L25.rectangle(L402 - L405 / 2 - 8, L403 - 48, 3, L404 + 10, 40, 40, 40, L406)
        L25.rectangle(L402 - L405 / 2 - 5, L403 - 48, 1, L404 + 9, 60, 60, 60, L406)
        L25.rectangle(L402 + L405 / 2 + 10, L403 - 53, 1, L404 + 20, 12, 12, 12, L406)
        L25.rectangle(L402 + L405 / 2 + 9, L403 - 52, 1, L404 + 18, 60, 60, 60, L406)
        L25.rectangle(L402 + L405 / 2 + 6, L403 - 48, 3, L404 + 10, 40, 40, 40, L406)
        L25.rectangle(L402 + L405 / 2 + 5, L403 - 48, 1, L404 + 10, 60, 60, 60, L406)
        L25.rectangle(L402 - L405 / 2 - 10, L403 - 48 + L404 + 14, L405 + 20, 1, 12, 12, 12, L406)
        L25.rectangle(L402 - L405 / 2 - 5, L403 - 51 + L404 + 12, L405 + 10, 1, 60, 60, 60, L406)
        L25.rectangle(L402 - L405 / 2 - 8, L403 - 52 + L404 + 14, L405 + 17, 3, 40, 40, 40, L406)
        L25.rectangle(L402 - L405 / 2 - 8, L403 - 49 + L404 + 14, L405 + 17, 1, 60, 60, 60, L406)
    end
end;
local L408 = 10 + (L22.sub(L24.get(L127.misc.settings.ref_dpiscale), 1, -2) - 100) / 25;
local L409 = L4.create_font('Lucida Console', L408, 400, { 0x080 })
local L410 = {}
function L410:new(L411, L412, L413)
    local L414 = { m_text = L411, m_color = L412, m_time = L413, lerped_pos = L2(L28.screen_size()).y }
    setmetatable(L414, self)
    self.__index = self;
    return L414
end;
local L415 = {}
function L415:new()
    local L416 = { m_notify_text = {} }
    setmetatable(L416, self)
    self.__index = self;
    return L416
end;
function L415:add(L417, L418, L419, L420, L421)
    L418 = L418 or { 255, 255, 255, 255 }
    L419 = L419 or 8.0;
    L420 = L132(L24.get(L90["misc"][3]), "console") or false;
    L421 = L421 or ""
    table.insert(self.m_notify_text, L410:new(L417, L418, L419))
    if L420 then
        if L421 == "fire" then
            L28.color_log(182, 231, 23, '[idealyaw] \0')
            L28.color_log(210, 210, 255, L417)
        else
            print(L417)
        end
    end
end;
function L415:think(L422, L423)
    local L424, L425, L426 = 8, 5, 12 + 1;
    local L427, L428 = L422[1] / 2, L422[2] / 2;
    local L429;
    local L430;
    local L431 = "c"
    local L432 = 1;
    local L433;
    if L423 == "small" then
        L431 = "-c"
    elseif L423 == "thin" then
        L431 = "c"
    elseif L423 == "bold" then
        L431 = "bc"
    elseif L423 == "blind" then
        L431 = "+c"
        L432 = 10
    end;
    if #self.m_notify_text > 6 then
        table.remove(self.m_notify_text, 1)
    end;
    for L434 = #self.m_notify_text, 1, -1 do
        local L435 = self.m_notify_text[L434]
        L435.m_time = L435.m_time - L26.frametime()
        if L435.m_time <= 0.0 then
            table.remove(self.m_notify_text, L434)
        end
    end;
    if #self.m_notify_text == 0 then
        return
    end;
    for L436, L437 in L9(self.m_notify_text) do
        L433 = L437.m_text;
        if L423 == "small" then
            L433 = L22.upper(L437.m_text)
        end;
        local L438 = { L25.measure_text(L431, L433) }
        L437.lerped_pos = L136(L437.lerped_pos, L422[2] / 2 + 300 + L436 * (23 + L438[2]), L26.frametime() * 10)
        smooth_center_y = L437.lerped_pos;
        L430 = L437.m_time;
        L429 = L437.m_color;
        if L430 < 0.5 then
            local L439 = L430;
            L439 = L23.min(L23.max(L439, 0.0), 0.5)
            L439 = L439 / 0.5;
            L429[4] = L23.floor(L439 * 255)
            if L436 == 1 and L439 < 0.2 then
                L425 = L425 - L426 * (1.0 - L439 / 0.2)
            end
        else
            L429[4] = 255
        end;
        if L409 and L132(L24.get(L90["misc"][3]), "default") then
            L4.draw_text(L424, L425, L429[1], L429[2], L429[3], L429[4], L409, L437.m_text)
        end;
        if L132(L24.get(L90["misc"][3]), "center") then
            gamesense_outer(L427, smooth_center_y, L438[2], L438[1], L429[4], true)
            smooth_center_y = smooth_center_y - 46;
            L25.gradient(L427 - L23.ceil(L438[1] / 2 + 3), smooth_center_y, L23.ceil(L438[1]) / 2, 1, 59, 175, 222, L429[4], 202, 70, 205, L429[4], true)
            L25.gradient(L427 - 4, smooth_center_y, L23.ceil(L438[1] / 2 + 7.5), 1, 202, 70, 205, L429[4], 204, 227, 53, L429[4], true)
            L25.gradient(L427 - L23.ceil(L438[1] / 2 + 3), smooth_center_y + 1, L23.ceil(L438[1]) / 2, 1, 59, 175, 222, L23.max(0, L23.min(255, L429[4])) - 100, 202, 70, 205, L429[4], true)
            L25.gradient(L427 - 4, smooth_center_y + 1, L23.ceil(L438[1] / 2 + 7.5), 1, 202, 70, 205, L429[4], 204, 227, 53, L23.max(0, L23.min(255, L429[4])) - 100, true)
            L25.text(L427, smooth_center_y + L438[2] - L432, 209, 209, 209, L429[4], L431, 0, L433)
        end;
        L425 = L425 + L426
    end
end;
g_notify = L415:new()
local L440 = { 'جدا الحمد لله أبي', "₩Ɽ₳ł₮Ⱨ ₴Ɇ₦Đ ₲ⱤɆɆ₮ł₦₲₴ ₱₳Ɽ₳ ₳ ₵Ø₦₳ Đ₳ ₮Ʉ₳ ₥₳̃Ɇ", "ஃᅔ>.< член в заднице у русских ＷＲＡＩＴＨ ＲＥＣＯＤＥᅕஃ", "ȶʏ ʄօʀ ʍ2 ƈօʍքɨӼɨօռ աɨȶɦ ȶɦɛ քօքֆ ǟռɖ ȶɦɛ ɮǟռɢֆ ʄȶ 𝔀𝓻𝓸𝓽𝓱 𝓵𝓸𝓪", "百萬富翁買鬼 ツ", "skeet invite code in morse: ... .-- ..-. -.-- -... .-- ..-. -... .--- --.. -... .-.. -.- .... ..-. .-.. -.- --. .. .-. .--. --. .-.. --.- --.- - -.-- .---- -..- . .-- -.- -.-- --.- ---.. .-.. .... ... ...- --.. -..- -.. .--. -..- -- -... - -.--", '𝟝𝟙.𝟙𝟟𝟠.𝟙𝟠𝟝.𝟚𝟛𝟛/𝕡𝕝𝕒𝕪𝕖𝕣𝕤.𝕛𝕤𝕠𝕟 𝓬𝓽𝓻𝓵+f "𝖎𝖘𝖘𝖔 𝖋𝖔𝖎 𝖉𝖔𝖕𝖊, 𝖌𝖆𝖓𝖉𝖆 𝖙𝖔𝖖𝖚𝖊"', "🕯️⧚🎃⧚🔮 ƙąYRཞơŋ ῳıƖƖ ƈơơ℘ ʂ℘ıɛƖɛŋ 🔮⧚🎃⧚🕯️", " ⓔⓜⓑⓡⓐⓒⓔ ⓡⓐⓒⓘⓢⓜ ", "yesterday i got smoked by (っ◔◡◔)っ ιвιzα 6ℓ 1.9 т∂ι 160 ¢υρяα 2004 160 нρ / 118 кω 1896 ¢м3 (115.7 ¢υ-ιи)", "【　ＷＲＡＩＴＨ　ＡＮＴＩ－ＡＩＭＢＯＴ　ＲＥＣＯＤＥ　】", "ʀᴀᴢ ᴀᴅᴅᴇᴅ ᴛʜɪs ᴛᴏ ᴡʀᴀɪᴛʜ ʀᴇᴄᴏᴅᴇ ᴀɴᴅ ɪᴛ ᴍᴀᴅᴇ ɪᴛ sᴏ ᴍᴜᴄʜ ʙᴇᴛᴛᴇʀ" }
last_random = 0;
new_random = 0;
textalhao = ""
say_time = 0;
ran = false;
local function L441(L442)
    if not L24.get(L90["misc"][4]) and not L24.get(L90["misc"][5]) then
        return
    end;
    local L443, L444 = L442.userid, L442.attacker;
    if L443 == nil or L444 == nil then
        return
    end;
    local L445 = L28.userid_to_entindex(L443)
    local L446 = L28.userid_to_entindex(L444)
    if L446 == L27.get_local_player() and L27.is_enemy(L445) then
        new_random = L28.random_int(1, #L440)
        while new_random == last_random do
            new_random = L28.random_int(1, #L440)
        end;
        textalhao = "say " .. L440[new_random]
        if L24.get(L90["misc"][5]) then
            say_time = L26.curtime()
            ran = false
        else
            L28.exec(textalhao)
        end;
        last_random = new_random
    end
end;
local L448 = function(L447)
    if not L447 then
        ran = false;
        return
    end;
    if L26.curtime() >= say_time + 1.5 and L26.curtime() <= say_time + 1.6 and not ran then
        L28.exec(textalhao)
        ran = true
    end
end;
local L453 = function(L449, L450, L451)
    if not L449 then
        return
    end;
    local L452 = cvar.cl_crosshairsize:get_int()
    final_dmg = L24.get(L127.rage.ref_min_damage_override[2]) and L24.get(L127.rage.ref_min_damage_override[3]) or L24.get(L127.rage.ref_min_damage[1])
    dmg_size = L25.measure_text("", final_dmg)
    L25.text(L450 / 2 + 10, L451 / 2 - 20, 255, 255, 255, 250, "", 0, final_dmg)
end;
local L460 = function(L454)
    local L455 = L27.get_local_player()
    local L456 = { L28.screen_size() }
    local L457 = L24.get(L90["visuals"][3])
    local L458 = L24.get(L90["visuals"][4])
    local L459 = L24.get(L90["visuals"][5])
    L448(L24.get(L90["misc"][4]) and L24.get(L90["misc"][5]))
    L453(L132(L24.get(L90["visuals"][6]), "min damage") and L27.is_alive(L455), L456[1], L456[2])
    watermark(L455, L458)
    L401(L454, L90["visuals"][0], L455, L456, L457)
    g_notify:think(L456, L459)
end;
local L463 = function(L461, L462)
    L462 = L462 or 1;
    L461 = L16.cast(L29, L461)
    return L16.cast('struct animation_layer_t**', L16.cast('char*', L461) + 0x2990)[0][L462]
end;
local L465 = function(L464)
    duckammount = L464.m_fDuckAmount;
    speedfraction = L23.max(0, L23.min(L464.m_flFeetSpeedForwardsOrSideWays, 1))
    speedfactor = L23.max(0, L23.min(1, L464.m_flFeetSpeedUnknownForwardOrSideways))
    unk1 = (L464.m_flStopToFullRunningFraction * -0.30000001 - 0.19999999) * speedfraction;
    unk2 = unk1 + 1;
    unk3 = 0;
    if duckammount > 0 then
        unk2 = unk2 + duckammount * speedfactor * (0.5 - unk2)
    end;
    unk3 = L464.m_flMaxYaw * unk2;
    return unk3
end;
local L472 = function(L466)
    local L467 = L32(L31, L466)
    local L468 = L33(L31, L466)
    local L469 = L16.cast(L29, L467)
    local L470 = L16.cast("char*", L469) + 0x9960;
    local L471 = L16.cast("struct animstate_t1**", L470)[0]
    if L467 == nil or L468 == nil or local_animstate == nil then
        return
    end;
    L466.set_prop(L466, "m_flPoseParameter", 1, 6)
end;
local L479 = function(L473)
    local L474 = L32(L31, L473)
    local L475 = L33(L31, L473)
    local L476 = L16.cast(L29, L474)
    local L477 = L16.cast("char*", L476) + 0x9960;
    local L478 = L16.cast("struct animstate_t1**", L477)[0]
    if L474 == nil or L475 == nil or L478 == nil then
        return
    end;
    if L26.chokedcommands() == 0 then
        L70.max_desync = L465(L478)
        L70.current_desync = L23.min(L23.max(L27.get_prop(L473, "m_flPoseParameter", 11) * 120 - 60, -58), 58)
        L70.current_desync = L70.current_desync > 0 and L23.ceil(L70.current_desync) or L23.floor(L70.current_desync)
    end;
    if L132(L24.get(L90["misc"][1]), "air walk") then
        if L2(L27.get_prop(L473, 'm_vecVelocity')):length2d() > 1.5 then
            ANIMATION_LAYER_MOVEMENT_MOVE = L463(L474, 6)
            ANIMATION_LAYER_MOVEMENT_MOVE.m_flWeight = 1
        end
    end;
    if L132(L24.get(L90["misc"][1]), "earthquake") then
        ANIMATION_LAYER_LEAN = L463(L474, 12)
        ANIMATION_LAYER_LEAN.m_flWeight = L28.random_float(0, 1)
    end;
    if L132(L24.get(L90["misc"][1]), "fake walk") and L70.in_speed then
        ANIMATION_LAYER_LEAN = L463(L474, 12)
        ANIMATION_LAYER_LEAN.m_flWeight = 0;
        ANIMATION_LAYER_MOVEMENT_MOVE = L463(L474, 6)
        ANIMATION_LAYER_MOVEMENT_MOVE.m_flWeight = 0
    end;
    if L132(L24.get(L90["misc"][1]), "blind") then
        ANIMATION_LAYER_FLASHED = L463(L474, 9)
        ANIMATION_LAYER_FLASHED.m_nSequence = 224;
        ANIMATION_LAYER_FLASHED.m_flWeight = 1
    end;
    if L132(L24.get(L90["misc"][1]), "moonwalk") then
        L27.set_prop(L473, 'm_flPoseParameter', 0, 7)
    end;
    if L132(L24.get(L90["misc"][1]), "smoothing") then
        L27.set_prop(L473, "m_flPoseParameter", 0, 2)
    end;
    if L132(L24.get(L90["misc"][1]), "fallen legs") then
        L27.set_prop(L473, "m_flPoseParameter", 1, 6)
    end;
    if L132(L24.get(L90["misc"][1]), "slide") then
        L27.set_prop(L473, "m_flPoseParameter", 1, 0)
    end;
    if L132(L24.get(L90["misc"][1]), "pitch on land") or true then
        if L478.m_bInHitGroundAnimation and L478.m_flHeadHeightOrOffsetFromHittingGroundAnimation > 0.101 and L478.m_bOnGround and not L28.key_state(0x20) then
            if L132(L24.get(L90["misc"][1]), "pitch on land") then
                L27.set_prop(L473, 'm_flPoseParameter', 0.5, 12)
            end;
            L70.landing = true
        else
            L70.landing = false
        end
    end
end;
local L480 = { ["3d sky"] = { cvar = cvar.r_3dsky, value = 1 }, ["fog"] = { cvars = { cvar.fog_enable, cvar.fog_enable_water_fog }, value = 1 }, ["shadows"] = { cvars = { cvar.r_shadows, cvar.cl_csm_static_prop_shadows, cvar.cl_csm_shadows, cvar.cl_csm_world_shadows, cvar.cl_foot_contact_shadows, cvar.cl_csm_viewmodel_shadows, cvar.cl_csm_rope_shadows, cvar.cl_csm_sprite_shadows, cvar.cl_csm_translucent_shadows, cvar.cl_csm_entity_shadows, cvar.cl_csm_world_shadows_in_viewmodelcascade }, value = 1 }, ["blood"] = { cvar = cvar.violence_hblood, value = 1 }, ["decals"] = { cvars = { cvar.r_drawdecals, cvar.r_drawropes, cvar.r_drawsprites }, value = 1 }, ["bloom"] = { cvar = cvar.mat_disable_bloom, value = 0 }, ["other"] = { cvars = { cvar.r_dynamic, cvar.r_eyegloss, cvar.r_eyes, cvar.r_drawtracers_firstperson, cvar.r_dynamiclighting }, value = 1 } }
local L491 = function()
    if not L24.get(L90["debug"][2]) then
        for L481, L482 in L10(L480) do
            if L482.cvar then
                if L482.cvar:get_int() ~= L482.value then
                    L482.cvar:set_int(L482.value)
                end
            else
                for L483, L484 in L9(L482.cvars) do
                    if L484:get_int() ~= L482.value then
                        L484:set_int(L482.value)
                    end
                end
            end
        end;
        return
    end;
    for L485, L486 in L10(L480) do
        if L132(L24.get(L90["debug"][3]), L485) then
            if L486.cvar then
                if L486.cvar:get_int() == L486.value then
                    L486.cvar:set_int(L486.value == 0 and 1 or (L486.value == 1 and 0 or L486.value))
                end
            else
                for L487, L488 in L9(L486.cvars) do
                    if L488:get_int() == L486.value then
                        L488:set_int(L486.value == 0 and 1 or (L486.value == 1 and 0 or L486.value))
                    end
                end
            end
        else
            if L486.cvar then
                if L486.cvar:get_int() ~= L486.value then
                    L486.cvar:set_int(L486.value)
                end
            else
                for L489, L490 in L9(L486.cvars) do
                    if L490:get_int() ~= L486.value then
                        L490:set_int(L486.value)
                    end
                end
            end
        end
    end
end;
local L493 = function()
    local L492 = L27.get_local_player()
    if not L27.is_alive(L492) then
        return
    end;
    L479(L492)
    L491()
end;
reset = function()
    L70.tickbase_max, L70.tickbase_diff = nil, nil;
    L70.old_tick_count = 0;
    L70.cur = 0;
    L70.banana = false;
    L70.bomb_defused = false;
    L70.bomb_exploded = false;
    local L494 = { cur = {}, prev = {} }
    local L495 = {}
    local L496 = {}
end;
reset()
local L498 = function(L497)
    L70.current_cmd = L497.command_number
end;
local L501 = function(L499)
    if L499.command_number == L70.current_cmd then
        L70.current_cmd = nil;
        local L500 = L27.get_prop(L27.get_local_player(), "m_nTickBase")
        if L70.tickbase_max ~= nil then
            L70.tickbase_diff = L500 - L70.tickbase_max
        end;
        L70.tickbase_max = L23.max(L500, L70.tickbase_max or 0)
    end
end;
local L503 = function(L502)
    return L23.floor(0.5 + L502 / L26.tickinterval())
end;
local L505 = function(L504)
    return L26.tickinterval() * L504
end;
local L506 = function()
    L70.fire_total_hits = 0;
    L70.post_total_hits = 0;
    L70.mode = "back"
    reset()
end;
local L512 = function(L507)
    if not L507 then
        return
    end;
    rage_fired = true;
    if L132(L24.get(L90["misc"][2]), "fire") then
        local L508 = L70.hitgroup_names[L507.hitgroup] or "?"
        local L509 = L507.target;
        local L510 = L26.tickcount() - L507.tick;
        local L511 = L23.min(L23.max(L27.get_prop(L509, "m_flPoseParameter", 11) * 120 - 60, -58), 58)
        g_notify:add(L22.format("fired at %s's %s for %i damage (%d%%) bt=%i (%ims) body=%iº", L27.get_player_name(L507.target), L508, L507.damage, L507.hit_chance, L510, L15(L510 * 1000), L511), { 210, 210, 255, 255 }, 5, nil, "fire")
    end;
    L70.fire_total_hits = L27.get_prop(L27.get_local_player(), "m_totalHitsOnServer")
    L70.handle_time = L26.realtime()
end;
local L518 = function(L513)
    if not L513 and (L132(L24.get(L90["misc"][2]), "damage") or L132(L24.get(L90["misc"][2]), "hurt") or L132(L24.get(L90["misc"][2]), "hurt self")) then
        return
    end;
    local L514 = L27.get_local_player()
    local L515 = L70.hitgroup_names[L513.hitgroup] or '?'
    local L516 = L28.userid_to_entindex(L513.userid)
    local L517 = L28.userid_to_entindex(L513.attacker)
    if L517 == L514 then
        if L132(L24.get(L90["misc"][2]), "damage") then
            g_notify:add(L22.format('hit %s in the %s for %d damage (%d health remaining)', L27.get_player_name(L516), L515, L513.dmg_health, L513.health), { 255, 255, 255, 255 }, 5)
        end
    elseif L517 == 0 and L516 == L514 then
        if L132(L24.get(L90["misc"][2]), "hurt self") then
            g_notify:add(L22.format("hurt yourself in the %s for %d damage (%d health remaining)", L515, L513.dmg_health, L513.health), { 255, 255, 255, 255 }, 5)
        end
    elseif L517 ~= 0 and L516 == L514 then
        if L132(L24.get(L90["misc"][2]), "hurt") then
            g_notify:add(L22.format("hurt by %s in the %s for %d damage (%d health remaining)", L27.get_player_name(L517), L515, L513.dmg_health, L513.health), { 255, 255, 255, 255 }, 5)
        end
    end
end;
local L520 = function(L519)
    if not L519 and L132(L24.get(L90["misc"][2]), "miss") then
        return
    end;
    L70.post_total_hits = L27.get_prop(L27.get_local_player(), 'm_totalHitsOnServer')
    if L519.reason == "?" then
        if L70.post_total_hits == L70.fire_total_hits + 1 and L70.post_total_hits < 255 and L70.fire_total_hits < 255 then
            L519.reason = "godmode"
        elseif L26.realtime() - L70.handle_time >= 0.5 then
            L519.reason = "delay"
        end
    end;
    g_notify:add(L22.format('missed shot due to %s', L519.reason), { 255, 255, 255, 255 }, 5)
end;
local function L521(L522)
    if not L132(L24.get(L90["misc"][2]), "fire") then
        return
    end;
    g_notify:add(L22.format("fired at %s's %s for %i damage (%d%%) bt=? (?ms) body=?º s=dormant", L27.get_player_name(L522.userid), L22.lower(L522.aim_hitbox), L522.dmg_health, L522.accuracy * 100), { 210, 210, 255, 255 }, 5, nil, "fire")
end;
local function L523(L524)
    if not L132(L24.get(L90["misc"][2]), "miss") then
        return
    end;
    g_notify:add(L22.format("fired at %s's %s for ? damage (%d%%) bt=? (?ms) body=?º s=dormant", L27.get_player_name(L524.userid), L22.lower(L524.aim_hitbox), L524.accuracy * 100), { 210, 210, 255, 255 }, 5)
    L28.delay_call(0.5, function()
        g_notify:add("missed shot due to dormant", nil, 5)
    end)
end;
local function L525(L526)
    if not L526 then
        return false
    end;
    return L70.mode ~= "back"
end;
local function L527(L528, L529)
    local L530 = { "CWorld", "CCSPlayer", "CFuncBrush", "CPhysicsPropMultiplayer", "CBaseEntity", "CC4" }
    local_origin = L2(L27.get_origin(L529))
    local L531, L532, L533 = L28.eye_position()
    local L534, L535 = L28.camera_angles()
    local L536 = L23.sin(L23.rad(L534))
    local L537 = L23.cos(L23.rad(L534))
    local L538 = L23.sin(L23.rad(L535))
    local L539 = L23.cos(L23.rad(L535))
    local L540 = { L537 * L539, L537 * L538, -L536 }
    local L541, L542 = L28.trace_line(L529, L531, L532, L533, L531 + L540[1] * 8192, L532 + L540[2] * 8192, L533 + L540[3] * 8192)
    local L543 = true;
    if L542 == -1 or L542 == nil or L529 == nil then
        return
    end;
    object_origin = L2(L27.get_origin(L542))
    local L544 = L23.abs(local_origin:dist2d(object_origin)) > 150;
    if L542 ~= nil then
        for L545 = 0, #L530 do
            if L27.get_classname(L542) == L530[L545] then
                L543 = false
            end
        end
    end;
    if L544 then
        L543 = false
    end;
    if not L543 and not L70.is_defusing and L528.in_use then
        L528.in_use = 0
    end
end;
local L550 = function(L546, L547)
    if not L547 or L27.is_dormant(L547) then
        return
    end;
    local L548 = L2(L27.get_origin(L547))
    local L549 = L2(L27.get_origin(L546))
    if L549:dist2d(L548) > 1400 and L2(L27.get_prop(L546, 'm_vecVelocity')):length2d() <= 150 then
        return true
    end;
    return false
end;
local L557 = function(L551, L552, L553)
    if not L552 or L27.is_dormant(L552) then
        return
    end;
    local L554 = { L27.get_origin(L552) }
    local L555 = { L27.get_origin(L551) }
    local L556 = L27.get_player_weapon(L551)
    if L555[3] > L554[3] + 55 and (L2(L27.get_prop(L551, 'm_vecVelocity')):length2d() <= 60 or L553.in_duck == 1) or L553.in_duck == 1 and L27.get_classname(L556) == "CKnife" then
        return true
    end;
    return false
end;
local L584 = function(L558, L559)
    if not L559 or L27.is_dormant(L559) then
        return
    end;
    local L560 = { L27.get_origin(L559) }
    local L561 = { L27.get_prop(L559, "m_vecViewOffset") }
    local L562 = { L28.eye_position() }
    local L563 = { L560[1] + L561[1], L560[2] + L561[2], L560[3] + L561[3] }
    local L564 = { L23.abs(L563[1] - L562[1]), L23.abs(L563[2] - L562[2]), L23.abs(L563[3] - L562[3]) }
    local L565 = L23.abs(L564[1] + L564[2])
    if L565 > 425 then
        return
    end;
    local L566 = { L27.get_prop(L558, 'm_vecVelocity') }
    local L567 = { L27.get_prop(L559, 'm_vecVelocity') }
    local L568 = L505(16)
    local L569 = { L562[1] + L566[1] * L568, L562[2] + L566[2] * L568, L562[3] + L566[3] * L568 }
    local L570 = { L563[1] + L567[1] * L568, L563[2] + L567[2] * L568, L563[3] + L567[3] * L568 }
    local L571, L572 = L28.trace_line(L558, L569[1], L569[2], L569[3], L570[1], L570[2], L570[3])
    local L573, L574 = L28.trace_line(L558, L570[1], L570[2], L570[3], L569[1], L569[2], L569[3])
    local L575, L576 = L28.trace_line(L558, L562[1], L562[2], L562[3], L563[1], L563[2], L563[3])
    local L577, L578 = L28.trace_line(L558, L562[1], L562[2], L562[3], L560[1], L560[2], L560[3])
    local L579 = L572 == L559 or L571 == 1;
    local L580 = L574 == L558 or L573 == 1;
    local L581 = L576 == L559 or L575 == 1;
    local L582 = L578 == L559 or L577 == 1;
    local L583 = L27.get_player_weapon(L559)
    if L27.get_classname(L583) == "CKnife" and (L579 or L580 or L581 or L582) then
        return true
    end;
    return false
end;
local L589 = function()
    local L585 = L27.get_players(true)
    if #L585 == 0 then
        L70.hittable = false;
        return
    end;
    for L586, L587 in L9(L585) do
        if L27.is_alive(L587) and not L27.is_dormant(L587) then
            local L588 = L27.get_esp_data(L587).flags or 0;
            if L21.band(L588, L21.lshift(1, 11)) ~= 0 then
                L70.hittable = true
            else
                L70.hittable = false
            end
        else
            L70.hittable = false
        end
    end;
    return false
end;
local L591 = function(L590)
    if L24.get(L127.anti_aim.other.ref_onshotantiaim[1]) and L24.get(L127.anti_aim.other.ref_onshotantiaim[2]) then
        return
    end;
    if not L24.get(L127.rage.ref_doubletap[1]) and not L24.get(L127.rage.ref_doubletap[2]) then
        return
    end;
    if L24.get(L90["misc"][8]) == "safest" then
        L70.defensive_risk = -4
    elseif L24.get(L90["misc"][8]) == "low" then
        L70.defensive_risk = -3
    elseif L24.get(L90["misc"][8]) == "medium" then
        L70.defensive_risk = -2
    elseif L24.get(L90["misc"][8]) == "high" then
        L70.defensive_risk = -1
    end;
    if L24.get(L90["misc"][6]) or L24.get(L90["misc"][7]) and L70.hittable then
        L590.force_defensive = 1;
        if L70.tickbase_diff == L70.defensive_risk then
            L24.set(L127.rage.ref_doubletap[1], false)
            L590.force_defensive = 0
        end
    else
        L590.force_defensive = 0;
        L24.set(L127.rage.ref_doubletap[1], true)
    end
end;
local L593 = function(L592)
    print(L70.tickbase_diff)
    if L3.get_double_tap() or L70.tickbase_diff ~= 1 and L24.get(L127.rage.ref_doubletap[1]) and L24.get(L127.rage.ref_doubletap[2]) then
        L592.force_defensive = 1;
        if L70.tickbase_diff ~= 1 then
            L24.set(L127.rage.ref_doubletap[1], false)
        end
    else
        L24.set(L127.rage.ref_doubletap[1], true)
    end
end;
local function L594(L595, L596, L597)
    local L598 = {
        {
            index = 13,
            condition = "backstab",
            check = function()
                return L584(L596, L597)
            end
        },
        {
            index = 16,
            condition = "legit",
            check = function()
                if L21.band(L595.buttons, 32) == 32 and not L70.is_defusing then
                    L527(L595, L596)
                    return true
                end
            end
        },
        {
            index = 11,
            condition = "manual",
            check = function()
                if L525(L132(L24.get(L90["anti-aim 2"][0]), "manual anti-aim") and L24.get(L90["anti-aim 2"][3])) then
                    return true
                end
            end
        },
        {
            index = 14,
            condition = "height",
            check = function()
                return L557(L596, L597, L595)
            end
        },
        {
            index = 15,
            condition = "high distance",
            check = function()
                return L550(L596, L597)
            end
        },
        {
            index = 12,
            condition = "freestanding",
            check = function()
                return false
            end
        },
        {
            index = 9,
            condition = "in fake duck",
            check = function()
                return L24.get(L127.rage.other.ref_fakeduck) and L21.band(L27.get_prop(L596, "m_fFlags"), 1) ~= 0
            end
        },
        {
            index = 10,
            condition = "fakelag",
            check = function()
                return not L24.get(L127.rage.ref_doubletap[2]) and not L24.get(L127.anti_aim.other.ref_onshotantiaim[2])
            end
        },
        {
            index = 5,
            condition = "in air",
            check = function()
                return (L70.jumping == true or L70.on_ground == false) and L595.in_duck == 0
            end
        },
        {
            index = 6,
            condition = "in air duck",
            check = function()
                return (L70.jumping == true or L70.on_ground == false) and L595.in_duck == 1
            end
        },
        {
            index = 8,
            condition = "in duck moving",
            check = function()
                return L595.in_duck == 1 and L2(L27.get_prop(L596, 'm_vecVelocity')):length2d() > 1.1
            end
        },
        {
            index = 7,
            condition = "in duck",
            check = function()
                return L595.in_duck == 1
            end
        },
        {
            index = 2,
            condition = "standing",
            check = function()
                return L2(L27.get_prop(L596, 'm_vecVelocity')):length2d() < 1.1
            end
        },
        {
            index = 4,
            condition = "slow motion",
            check = function()
                return L24.get(L127.anti_aim.other.ref_slowmotion[1]) and L24.get(L127.anti_aim.other.ref_slowmotion[2])
            end
        },
        {
            index = 3,
            condition = "moving",
            check = function()
                return L2(L27.get_prop(L596, 'm_vecVelocity')):length2d() > 1.1 and L21.band(L27.get_prop(L596, "m_fFlags"), 1) == 1
            end
        }
    }
    for L599, L600 in L9(L598) do
        if L600.check() then
            if L24.get(L90["anti-aim"][0]) == "gamesense" then
                if L80 ~= nil and L24.get(L80[L600.index][0]) then
                    if L24.get(L80[L600.index][12]) and L24.get(L90["anti-aim 2"][2]) then
                        if L24.get(L80[12][0]) then
                            return "freestanding", 12
                        else
                            return "freestanding", 1
                        end
                    end;
                    return L600.condition, L600.index
                end
            end
        end
    end;
    if L80 ~= nil and L24.get(L80[1][0]) then
        return "global", 1
    end;
    return "invalid", -1
end;
local L610 = function(L601, L602, L603, L604)
    if not L604 then
        return
    end;
    L70.current_condition, L70.current_condition_index = L594(L601, L602, L603)
    if L70.current_condition == "invalid" then
        L148()
        return
    end;
    if L24.get(L90["anti-aim"][0]) == "gamesense" then
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[1], L24.get(L80[L70.current_condition_index][1]))
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[2], L24.get(L80[L70.current_condition_index][2]))
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_base, L24.get(L80[L70.current_condition_index][3]))
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[1], L24.get(L80[L70.current_condition_index][4]))
        if L70.current_condition == "manual" then
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand[1], false)
            if L70.mode == "left" then
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], -L24.get(L90["anti-aim 2"][8]))
            elseif L70.mode == "right" then
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L24.get(L90["anti-aim 2"][9]))
            elseif L70.mode == "forward" then
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], 180)
            end
        else
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L24.get(L80[L70.current_condition_index][5]))
        end;
        if L24.get(L80[L70.current_condition_index][6]) ~= "slow" then
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1], L24.get(L80[L70.current_condition_index][6]))
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[2], L24.get(L80[L70.current_condition_index][7]))
        else
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1], "Off")
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[2], 0)
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L70.fake_fakelag >= 3 and -L24.get(L80[L70.current_condition_index][7]) / 2 or L24.get(L80[L70.current_condition_index][7]) / 2)
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[1], "static")
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[2], L70.fake_fakelag >= 3 and -180 or 180)
        end;
        if L24.get(L80[L70.current_condition_index][6]) ~= "slow" then
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[1], L24.get(L80[L70.current_condition_index][8]))
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_body_yaw[2], L24.get(L80[L70.current_condition_index][9]))
        end;
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand_body, L24.get(L80[L70.current_condition_index][10]))
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_edge_yaw, L24.get(L80[L70.current_condition_index][11]))
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_roll, L24.get(L80[L70.current_condition_index][13]))
        if L70.current_condition == "freestanding" then
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand[1], true)
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_edge_yaw, false)
        else
            L24.set(L127.anti_aim.anti_aimbot_angles.ref_freestand[1], false)
        end;
        if L24.get(L80[L70.current_condition_index][14]) then
            L601.force_defensive = 1
        end;
        if L26.chokedcommands() < 13 and L70.tickbase_diff ~= nil and L70.tickbase_diff ~= 1 and L70.tickbase_diff < -2 then
            local L605 = L80[L70.current_condition_index]
            local L606 = L24.get(L605[15])
            local L607 = L24.get(L605[16])
            if L606 ~= "off" and L606 ~= "zero" then
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[1], L606)
            else
                if L606 == "zero" then
                    L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[1], "custom")
                    L24.set(L127.anti_aim.anti_aimbot_angles.ref_pitch[2], 0)
                end
            end;
            if L607 ~= "off" then
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[1], "180")
                L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw_jitter[1], "off")
                if L607 == "forward" then
                    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], 180)
                elseif L607 == "spin" then
                    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L110(L138(L70.yaw_increment_spin), -180, 180))
                elseif L607 == "jitter" then
                    L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L70.banana and 90 or -90)
                elseif L607 == "opposite" then
                    local L608 = { forward = 0, left = 90, right = -90 }
                    local L609 = L608[L70.mode]
                    if L609 ~= nil then
                        L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[2], L609)
                    end
                end
            end
        end;
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_yaw[1], L24.get(L80[L70.current_condition_index][4]))
    else
        if L24.get(L90["anti-aim"][0]) == "idealyaw" then
            L148()
        end
    end
end;
local L615 = function(L611)
    local_origin = L2(L27.get_origin(L611))
    local L612 = nil;
    local L613 = L2(L27.get_prop(L27.get_all("CPlantedC4")[1], "m_vecOrigin"))
    if L613.x ~= nil then
        L612 = local_origin:dist(L613)
    else
        L612 = nil
    end;
    local L614 = L27.get_prop(L611, "m_iTeamNum")
    L70.is_defusing = L614 == 3 and L612 < 60 and not L70.bomb_defused and not L70.bomb_exploded
end;
local L619 = function(L616)
    local L617 = L27.get_local_player()
    local L618 = L28.current_threat()
    if L24.get(L90["debug"][0]) and L86.is_hovered or L157.dragging then
        L616.in_attack = false
    end;
    L70.on_ground = L21.band(L27.get_prop(L617, "m_fFlags"), 1) == 1;
    L70.jumping = L24.get(L127.misc.movement.ref_bhop) and L616.in_jump == 1;
    L70.in_speed = L21.band(L616.buttons, 131072) > 0;
    L589()
    L591(L616)
    L615(L617)
    if L26.chokedcommands() == 0 then
        L70.current_desync = L23.min(L23.max(L27.get_prop(L617, "m_flPoseParameter", 11) * 120 - 60, -58), 58)
        L70.current_desync = L70.current_desync > 0 and L23.ceil(L70.current_desync) or L23.floor(L70.current_desync)
    end;
    if L26.chokedcommands() == 0 then
        L70.fake_fakelag = L70.fake_fakelag + 1;
        if L70.fake_fakelag >= 6 then
            L70.fake_fakelag = 0
        end
    end;
    L610(L616, L617, L618, true)
end;
local L624 = function()
    if not L86.is_open then
        L86.mouse_press = false;
        return
    end;
    local L620 = L24.get(L127.misc.settings.ref_dpiscale)
    local L621 = { L24.menu_size() }
    local L622 = { L24.menu_position() }
    local L623 = { L24.mouse_position() }
    scale = { 0, 0 }
    scale_x = 0;
    if L620 == "100%" then
        scale = { L86.dpi_scaling_y[1][1], L86.dpi_scaling_y[1][2] }
        scale_x = 76
    elseif L620 == "125%" then
        scale = { L86.dpi_scaling_y[2][1], L86.dpi_scaling_y[2][2] }
        scale_x = 95
    elseif L620 == "150%" then
        scale = { L86.dpi_scaling_y[3][1], L86.dpi_scaling_y[3][2] }
        scale_x = 113
    elseif L620 == "175%" then
        scale = { L86.dpi_scaling_y[4][1], L86.dpi_scaling_y[4][2] }
        scale_x = 132
    elseif L620 == "200%" then
        scale = { L86.dpi_scaling_y[5][1], L86.dpi_scaling_y[5][2] }
        scale_x = 151
    end;
    if L28.key_state(0x1) then
        if not L86.mouse_press then
            L86.mouse_press = true;
            if L623[1] > L622[1] + 5 and L623[1] < L622[1] + 5 + scale_x then
                if L623[2] > L622[2] + scale[1] and L623[2] < L622[2] + scale[2] then
                    L86.selected_gs_tab = true
                elseif L623[2] > L622[2] + 19 or L623[2] < L622[2] + L621[2] and (L623[2] < L622[2] + scale[1] and L623[2] > L622[2] + scale[2]) and L623[2] < L622[2] + L621[2] and L86.selected_gs_tab == true then
                    L86.selected_gs_tab = false
                end
            end
        end
    else
        L86.mouse_press = false
    end
end;
local L629 = function()
    if L27.get_prop(L27.get_local_player(), "m_MoveType") == 8 then
        L70.current_condition_index = 17;
        L70.current_condition = "noclip"
    end;
    local L625 = { ["left"] = L90["anti-aim 2"][4], ["right"] = L90["anti-aim 2"][5], ["forward"] = L90["anti-aim 2"][6], ["back"] = L90["anti-aim 2"][7] }
    local L626;
    for L627, L628 in L10(L625) do
        if L24.get(L628) and L70[L627 .. "_ready"] then
            L626 = L627 == L70.mode and "back" or L627;
            L70[L627 .. "_ready"] = false
        end;
        if not L24.get(L628) then
            L70[L627 .. "_ready"] = true
        end
    end;
    L70.mode = L626 or L70.mode
end;
local L630 = function()
    L70.cur = L26.tickcount()
    if L70.cur > L70.old_tick_count then
        L70.banana = not L70.banana;
        L70.old_tick_count = L70.cur + 1
    end;
    L70.yaw_increment_spin = L70.yaw_increment_spin + 20;
    if L70.yaw_increment_spin >= 1080 then
        L70.yaw_increment_spin = 0
    end;
    if L70.started == 10 then
        if L70.pulse >= 10 then
            L70.pulse = L70.pulse + 2.5
        end;
        if L70.pulse >= 240 then
            L70.started = 1
        end
    end;
    if L70.started == 1 then
        L70.pulse = L70.pulse - 2.5;
        if L70.pulse <= 10 then
            L70.started = 10
        end
    end
end;
local L647 = function(L631)
    local L632 = L27.get_players(true)
    if #L632 == 0 then
        L71 = { cur = {}, prev = {}, pre_prev = {}, pre_pre_prev = {} }
        return nil
    end;
    for L633, L634 in L9(L632) do
        if L27.is_alive(L634) and not L27.is_dormant(L634) then
            local L635 = 0;
            local L636 = L27.get_esp_data(L634).flags or 0;
            if L21.band(L636, L21.lshift(1, 17)) ~= 0 then
                L635 = L503(L27.get_prop(L634, "m_flSimulationTime")) - 14
            else
                L635 = L503(L27.get_prop(L634, "m_flSimulationTime"))
            end;
            if L71.cur[L634] == nil or L635 - L71.cur[L634].simtime >= 1 then
                L71.pre_pre_prev[L634] = L71.pre_prev[L634]
                L71.pre_prev[L634] = L71.prev[L634]
                L71.prev[L634] = L71.cur[L634]
                local L637 = L2(L27.get_prop(L631, "m_vecOrigin"))
                local L638 = L2(L27.get_prop(L634, "m_angEyeAngles"))
                local L639 = L2(L27.get_prop(L634, "m_vecOrigin"))
                local L640 = L23.floor(L138(L638.y - calculate_angle(L637, L639)))
                local L641 = L27.get_prop(L634, "m_flDuckAmount")
                local L642 = L21.band(L27.get_prop(L634, "m_fFlags"), 1) == 1;
                local L643 = L2(L27.get_prop(L634, 'm_vecVelocity')):length2d()
                local L644 = L642 and (L641 == 1 and "duck" or (L643 > 1.2 and "running" or "standing")) or "air"
                local L645 = L27.get_player_weapon(L634)
                local L646 = L27.get_prop(L645, "m_fLastShotTime")
                L71.cur[L634] = { id = L634, origin = L2(L27.get_origin(L634)), pitch = L638.x, yaw = L640, yaw_backwards = L23.floor(L138(calculate_angle(L637, L639))), simtime = L635, stance = L644, esp_flags = L27.get_esp_data(L634).flags or 0, last_shot_time = L646 }
            end
        end
    end
end;
local L648 = false;
local L672 = function(L649)
    if not L27.is_alive(L649) then
        if L648 then
        end;
        L648 = false;
        return
    end;
    local L650 = L27.get_players(true)
    if #L650 == 0 then
        return nil
    end;
    for L651, L652 in L9(L650) do
        if L27.is_alive(L652) and not L27.is_dormant(L652) then
            if L71.cur[L652] ~= nil and L71.prev[L652] ~= nil and L71.pre_prev[L652] ~= nil and L71.pre_pre_prev[L652] ~= nil then
                local L653 = nil;
                local L654 = nil;
                local L655;
                local L656;
                local L657 = L23.abs(L138(L71.cur[L652].yaw - L71.prev[L652].yaw))
                local L658 = L138(L71.cur[L652].yaw - L71.prev[L652].yaw)
                if L71.cur[L652].last_shot_time ~= nil then
                    L655 = L26.curtime() - L71.cur[L652].last_shot_time;
                    L656 = L655 / L26.tickinterval()
                    L654 = L656 <= L23.floor(0.2 / L26.tickinterval())
                end;
                if L24.get(L90["debug"][1]) == "desync" then
                    L648 = true;
                    local L659 = L71.cur[L652].yaw;
                    local L660 = L71.prev[L652].yaw;
                    local L661 = L71.pre_prev[L652].yaw;
                    local L662 = L71.pre_pre_prev[L652].yaw;
                    local L663 = L138(L659 - L660)
                    local L664 = L138(L659 - L661)
                    local L665 = L138(L660 - L662)
                    local L666 = L138(L660 - L661)
                    local L667 = L138(L661 - L662)
                    local L668 = L138(L662 - L659)
                    local L669 = L138(L657 - L668)
                    if L654 and L23.abs(L23.abs(L71.cur[L652].pitch) - L23.abs(L71.prev[L652].pitch)) > 30 and L71.cur[L652].pitch < L71.prev[L652].pitch then
                        L653 = "ON SHOT"
                    else
                        if L23.abs(L71.cur[L652].pitch) > 60 then
                            if L657 > 30 and L23.abs(L664) < 15 and L23.abs(L665) < 15 then
                                L653 = "[!!]"
                            elseif L23.abs(L663) > 15 or L23.abs(L666) > 15 or L23.abs(L667) > 15 or L23.abs(L668) > 15 then
                                L653 = "[!!!]"
                            end
                        end
                    end;
                    if L24.get(L90["debug"][5]) and L24.get(L90["debug"][6]) then
                        if L653 ~= "ON SHOT" then
                            L18.set(L652, "Add to whitelist", true)
                        else
                            L18.set(L652, "Add to whitelist", false)
                        end
                    else
                        L18.set(L652, "Add to whitelist", false)
                    end;
                    if L147[L652] and L653 ~= nil then
                        if L71.cur[L652].stance == "standing" and #L73[L652].stand < 20 then
                            table.insert(L73[L652].stand_type, L653)
                            if L653 == "[!!!]" and L657 > 5 then
                                table.insert(L73[L652].stand, L657)
                            else
                                if L653 == "[!!]" then
                                    table.insert(L73[L652].stand, L657)
                                end
                            end
                        elseif L71.cur[L652].stance == "running" and #L73[L652].run < 20 then
                            table.insert(L73[L652].run_type, L653)
                            if L653 == "[!!!]" and L657 > 5 then
                                table.insert(L73[L652].run, L657)
                            else
                                if L653 == "[!!]" then
                                    table.insert(L73[L652].run, L657)
                                end
                            end
                        elseif L71.cur[L652].stance == "air" and #L73[L652].air < 20 then
                            table.insert(L73[L652].air_type, L653)
                            if L653 == "[!!!]" and L657 > 5 then
                                table.insert(L73[L652].air, L657)
                            else
                                if L653 == "[!!]" then
                                    table.insert(L73[L652].air, L657)
                                end
                            end
                        elseif L71.cur[L652].stance == "duck" and #L73[L652].duck < 20 then
                            table.insert(L73[L652].duck_type, L653)
                            if L653 == "[!!!]" and L657 > 5 then
                                table.insert(L73[L652].duck, L657)
                            else
                                if L653 == "[!!]" then
                                    table.insert(L73[L652].duck, L657)
                                end
                            end
                        end
                    end;
                    if L71.cur[L652].pitch >= 78 and L71.prev[L652].pitch > 78 then
                        if L653 == "[!!!]" or L653 == "[!!]" then
                            if L653 == "[!!]" then
                                if L138(L659 - L660) > 0 then
                                    L18.set(L652, "Force body yaw", true)
                                    L18.set(L652, "Force body yaw value", 60)
                                elseif L138(L659 - L660) < 0 then
                                    L18.set(L652, "Force body yaw", true)
                                    L18.set(L652, "Force body yaw value", -60)
                                end
                            elseif L653 == "[!!!]" then
                                local L670 = 0;
                                local L671 = 0;
                                if (L660 == L138(L659 - L657) or L660 == L138(L659 + L657)) and (L661 == L138(L659 + L657) or L661 == L659) and (L661 == L138(L659 + L657) or L661 == L659) then
                                    L18.set(L652, "Force body yaw", true)
                                    L18.set(L652, "Force body yaw value", 0)
                                    L670 = L659
                                else
                                    if L659 ~= L670 then
                                        if L659 < 0 then
                                            L18.set(L652, "Force body yaw", true)
                                            L18.set(L652, "Force body yaw value", 60)
                                        else
                                            L18.set(L652, "Force body yaw", true)
                                            L18.set(L652, "Force body yaw value", -60)
                                        end
                                    end
                                end
                            end
                        else
                            L18.set(L652, "Force body yaw", false)
                            L18.set(L652, "Force body yaw value", 0)
                        end
                    end
                elseif L24.get(L90["debug"][1]) == "---" then
                    L653 = nil;
                    L648 = true;
                    break
                elseif L24.get(L90["debug"][1]) == "off" then
                    if L648 then
                        L653 = nil;
                        L24.set(L127.plist.reset, true)
                        L18.set(L652, "Force body yaw", false)
                        L18.set(L652, "Force body yaw value", 0)
                        L648 = false
                    end
                end;
                L72[L652] = { anti_aim_type = L653, yaw_delta = L658 }
            end
        else
            m_fired = false;
            time_difference = 0;
            ticks_since_last_shot = 0
        end
    end
end;
local L674 = function(L673)
    L673 = L27.get_local_player()
    if not L24.get(L76) then
        return
    end;
    if L132(L24.get(L90["misc"][1]), "fake duck") then
        L27.set_prop(L673, "m_flPoseParameter", 1, 1)
    end;
    L630()
    L647(L673)
    L672(L673)
end;
L28.register_esp_flag("", 255, 255, 255, function(L675)
    if not L27.is_alive(L27.get_local_player()) then
        return
    end;
    if L24.get(L90["debug"][1]) then
        if L27.is_alive(L675) and not L27.is_dormant(L675) then
            if L72[L675] ~= nil then
                if L72[L675].anti_aim_type ~= nil then
                    return true, "\affffffc8" .. L22.upper(L72[L675].anti_aim_type)
                end
            end
        end
    end
end)
local L690 = function()
    if not L24.get(L90["debug"][0]) or not L24.get(L76) then
        L86.menu_alpha = 0;
        L86.is_hovered = false;
        L88 = false;
        return
    end;
    local L676 = L24.get(L127.misc.settings.ref_dpiscale)
    L86.height = L89[L676] or 68;
    if L24.get(L127.misc.settings.ref_menukey) then
        if not L87 then
            L87 = true;
            L86.is_open = not L86.is_open;
            L88 = false
        end
    else
        L87 = false
    end;
    if not L24.is_menu_open() then
        L86.is_open = false
    end;
    if not L88 then
        L86.fade_start_time = L86.is_open and L26.realtime() or L26.realtime()
        L88 = true
    end;
    if not L86.selected_gs_tab then
        L86.menu_alpha = 0
    end;
    local L677 = L86.is_open and L86.selected_gs_tab and 255 or 0;
    local L678 = L26.realtime() - L86.fade_start_time;
    local L679 = L23.min(1, L678 / 0.5)
    L86.menu_alpha = L136(L86.menu_alpha, L677, L679)
    if L86.menu_alpha <= 0 then
        L86.is_hovered = false;
        return
    end;
    local L680 = { L24.menu_size() }
    local L681 = L23.ceil((L680[1] - 12) / #L86.tabs_names)
    local L682 = { L24.menu_position() }
    local L683 = { L24.mouse_position() }
    L86.is_hovered = L683[1] > L682[1] and L683[1] < L682[1] + L681 * #L86.tabs_names and L683[2] > L682[2] - L86.height and L683[2] < L682[2] - L86.height + L86.height;
    for L684, L685 in L9(L86.tabs_names) do
        local L686 = L682[1] + 6 + L681 * (L684 - 1)
        local L687 = L683[1] > L686 and L683[1] < L686 + L681 and L683[2] > L682[2] - L86.height and L683[2] < L682[2]
        if L86.selected_tab == L684 then
            L86.selected_color[1] = { 20, 20, 20 }
            L86.selected_color[2] = { 210, 210, 210 }
        else
            L86.selected_color[1] = { 12, 12, 12 }
            L86.selected_color[2] = { 90, 90, 90 }
        end;
        if L687 and L86.selected_tab ~= L684 then
            L86.selected_color[1] = { 12, 12, 12 }
            L86.selected_color[2] = { 167, 167, 167 }
        end;
        L25.rectangle(L686, L682[2] - L86.height, L681, L86.height, L86.selected_color[1][1], L86.selected_color[1][2], L86.selected_color[1][3], L86.menu_alpha)
        L25.text(L686 + L681 / 2, L682[2] - L86.height / 2, L86.selected_color[2][1], L86.selected_color[2][2], L86.selected_color[2][3], L86.menu_alpha, "c+d", 0, L684 == 6 and L85[L24.get(L90["debug"][4])] or L685)
        if L687 and L28.key_state(0x1) then
            L86.selected_tab = L684;
            for L688, L689 in L9(L81) do
                if L86.selected_tab == L688 then
                    L24.set(L90.tab, L689)
                end
            end
        end
    end;
    gamesense_outer(L682[1], L682[2], L680[1], L86.height, L86.menu_alpha, false)
end;
local L691 = L24.new_label("Players", "Adjustments", "-")
local L692 = L24.new_label("Players", "Adjustments", "-")
local function L693()
    local L694 = L24.get(L127.plist.players)
    if L694 == nil then
        return
    end;
    if not L147[L694] then
        g_notify:add("[STEALER] Please enable 'scan anti-aim'.", nil, 5)
        return
    end;
    if L146[L694] then
        if #L73[L694].stand >= 20 or #L73[L694].run >= 20 or #L73[L694].air >= 20 or #L73[L694].duck >= 20 then
            if #L73[L694].stand >= 20 then
                local L695 = L126(L73[L694].stand_type)
                local L696 = L126(L73[L694].stand)
                if L695 == "[!!]" then
                    L695 = "Center"
                elseif L695 == "[!!!]" then
                    L695 = "Skitter"
                end;
                L24.set(L80[2][6], L695)
                L24.set(L80[2][7], L696)
            end;
            if #L73[L694].run >= 20 then
                local L697 = L126(L73[L694].run_type)
                local L698 = L126(L73[L694].run)
                if L697 == "[!!]" then
                    L697 = "Center"
                elseif L697 == "[!!!]" then
                    L697 = "Skitter"
                end;
                L24.set(L80[3][6], L697)
                L24.set(L80[3][7], L698)
            end;
            if #L73[L694].air >= 20 then
                local L699 = L126(L73[L694].air_type)
                local L700 = L126(L73[L694].air)
                if L699 == "[!!]" then
                    L699 = "Center"
                elseif L699 == "[!!!]" then
                    L699 = "Skitter"
                end;
                L24.set(L80[5][6], L699)
                L24.set(L80[5][7], L700)
            end;
            if #L73[L694].duck >= 20 then
                local L701 = L126(L73[L694].duck_type)
                local L702 = L126(L73[L694].duck)
                if L701 == "[!!]" then
                    L701 = "Center"
                elseif L701 == "[!!!]" then
                    L701 = "Skitter"
                end;
                L24.set(L80[7][6], L701)
                L24.set(L80[7][7], L702)
            end
        else
            g_notify:add("[STEALER] At least one stance must be done", nil, 5)
        end
    else
        if #L73[L694].stand ~= 20 then
            g_notify:add("[STEALER] Still scanning standing anti-aim", nil, 5)
            return
        end;
        if #L73[L694].run ~= 20 then
            g_notify:add("[STEALER] Still scanning running anti-aim", nil, 5)
            return
        end;
        if #L73[L694].air ~= 20 then
            g_notify:add("[STEALER] Still scanning air anti-aim", nil, 5)
            return
        end;
        if #L73[L694].duck ~= 20 then
            g_notify:add("[STEALER] Still scanning duck anti-aim", nil, 5)
            return
        end;
        if #L73[L694].stand >= 20 then
            local L703 = L126(L73[L694].stand_type)
            local L704 = L126(L73[L694].stand)
            if L703 == "[!!]" then
                L703 = "Center"
            elseif L703 == "[!!!]" then
                L703 = "Skitter"
            end;
            L24.set(L80[2][6], L703)
            L24.set(L80[2][7], L704)
        end;
        if #L73[L694].run >= 20 then
            local L705 = L126(L73[L694].run_type)
            local L706 = L126(L73[L694].run)
            if L705 == "[!!]" then
                L705 = "Center"
            elseif L705 == "[!!!]" then
                L705 = "Skitter"
            end;
            L24.set(L80[3][6], L705)
            L24.set(L80[3][7], L706)
        end;
        if #L73[L694].air >= 20 then
            local L707 = L126(L73[L694].air_type)
            local L708 = L126(L73[L694].air)
            if L707 == "[!!]" then
                L707 = "Center"
            elseif L707 == "[!!!]" then
                L707 = "Skitter"
            end;
            L24.set(L80[5][6], L707)
            L24.set(L80[5][7], L708)
        end;
        if #L73[L694].duck >= 20 then
            local L709 = L126(L73[L694].duck_type)
            local L710 = L126(L73[L694].duck)
            if L709 == "[!!]" then
                L709 = "Center"
            elseif L709 == "[!!!]" then
                L709 = "Skitter"
            end;
            L24.set(L80[7][6], L709)
            L24.set(L80[7][7], L710)
        end
    end;
    g_notify:add("[STEALER] Imported anti-aim settings from: " .. L27.get_player_name(L694), nil, 5)
end;
local L712 = function()
    local L711 = L24.get(L127.plist.players)
    if L711 then
        if L147[L711] then
            perc_stand = #L73[L711].stand / 20 * 100;
            perc_run = #L73[L711].run / 20 * 100;
            perc_air = #L73[L711].air / 20 * 100;
            perc_duck = #L73[L711].duck / 20 * 100;
            steal_string = perc_stand .. "% - " .. perc_run .. "% - " .. perc_air .. "% - " .. perc_duck .. "%"
            L24.set(L691, L22.format("%s", steal_string))
            L24.set(L692, L22.format("%s", "stand - run - air - duck"))
            if L146[L711] then
                if perc_stand == 100 or perc_run == 100 or perc_air == 100 or perc_duck == 100 then
                    L24.set(L691, L22.format('%s', "done!"))
                end
            else
                if perc_stand == 100 and perc_run == 100 and perc_air == 100 and perc_duck == 100 then
                    L24.set(L691, L22.format('%s', "done!"))
                end
            end
        else
            L24.set(L691, L22.format('%s', "waiting for scan..."))
            L73[L711].stand = {}
            L73[L711].stand_type = {}
            L73[L711].run = {}
            L73[L711].run_type = {}
            L73[L711].air = {}
            L73[L711].air_type = {}
            L73[L711].duck = {}
            L73[L711].duck_type = {}
        end
    end
end;
local L713 = L24.new_button("Players", "Adjustments", "import anti-aim", L693)
local L714 = false;
local L734 = function()
    local L715 = L24.get(L76)
    local L716 = false;
    local L717 = L24.get(L90.tab)
    local L718 = L24.get(L90["anti-aim"][0])
    local L719 = L24.get(L90["anti-aim"][1])
    L690()
    if not L24.is_menu_open() then
        return
    end;
    L624()
    L154(L715)
    if not L715 then
        if not L70.reset_once then
            L148()
            L70.reset_once = true
        end;
        L70.smooth_idealyaw = -1080;
        L70.smooth_dt = -1080;
        L70.smooth_os = -1080;
        L70.smooth_pc = -1080;
        L70.smooth_bo = -1080;
        L70.smooth_idealyaw_recode = -1080;
        L70.smooth_dt_2 = -1080;
        L70.smooth_stance = -1080;
        L70.dt_os_text_anim = 0;
        L70.current_cond_text_anim = 0
    else
        L24.set(L127.anti_aim.anti_aimbot_angles.ref_aa_enabled, true)
        L70.reset_once = false
    end;
    if L717 == "config" then
        L24.update(L90["config"][1], update_cfg())
    end;
    L24.set_visible(L90.tab, L715 and L24.get(L90["debug"][0]) == false)
    L712()
    if L24.get(L90["debug"][1]) ~= "off" then
        L24.set_visible(L127.plist.force_body, false)
        L24.set_visible(L127.plist.force_body_value, false)
        L714 = true
    else
        if L714 then
            L24.set_visible(L127.plist.force_body, true)
            L24.set_visible(L127.plist.force_body_value, true)
            local L720 = L27.get_players(true)
            if #L720 ~= 0 then
                for L721, L722 in L9(L720) do
                    L18.set(L722, "Force body yaw", false)
                    L18.set(L722, "Force body yaw value", 0)
                end
            end;
            L714 = false
        end
    end;
    for L723, L724 in L10(L90) do
        if L724 ~= L90.tab then
            for L725, L726 in L10(L724) do
                L24.set_visible(L726, L715 and L723 == L717)
                if L717 == "anti-aim 2" then
                    for L727 = 1, 9 do
                        if L727 == 1 or L727 == 2 then
                            L24.set_visible(L90["anti-aim 2"][L727], L715 and L132(L24.get(L90["anti-aim 2"][0]), "other anti-aim binds"))
                        elseif L727 > 2 and L727 < 10 then
                            L24.set_visible(L90["anti-aim 2"][L727], L715 and L132(L24.get(L90["anti-aim 2"][0]), "manual anti-aim"))
                        end
                    end
                end;
                if L717 == "visuals" then
                    L24.set_visible(L90["visuals"][4], L715 and L24.get(L90["visuals"][2]))
                    L24.set_visible(L90["visuals"][5], L715 and L24.get(L90["visuals"][7]))
                    if not L132(L24.get(L90["misc"][3]), "default") and not L132(L24.get(L90["misc"][3]), "center") then
                        L24.set_visible(L90["visuals"][5], L715 and false)
                        L24.set_visible(L90["visuals"][7], L715 and false)
                    end
                end;
                if L717 == "misc" then
                    L24.set_visible(L90["misc"][5], L715 and L24.get(L90["misc"][4]))
                end;
                if L717 == "debug" then
                    L24.set_visible(L90["debug"][3], L715 and L24.get(L90["debug"][2]))
                end
            end
        end
    end;
    for L728, L729 in L9({ L82, L83 }) do
        L78 = L729;
        for L730, L731 in L10(L729) do
            if L718 == "gamesense" and L729 == L82 then
                L80 = L729
            elseif L718 == "idealyaw" and L729 == L83 then
                L79 = L729
            end;
            for L732, L733 in L10(L731) do
                L716 = (L718 == "gamesense" and L729 == L82 or L718 == "idealyaw" and L729 == L83) and L84[L730] == L719 and L717 == "anti-aim" and L715 and (L733 == L729[L730][0] or L24.get(L729[L730][0]))
                if L718 == "gamesense" and L729 == L82 then
                    if L719 == "freestanding" or L719 == "manual" or L719 == "legit" or L719 == "backstab" then
                        L716 = L716 and (L733 ~= L729[L730][11] and L733 ~= L729[L730][12])
                    end;
                    if L719 == "manual" then
                        L716 = L716 and L733 ~= L729[L730][5]
                    end;
                    if L24.get(L729[L730][1]) ~= "custom" then
                        L716 = L716 and L733 ~= L729[L730][2]
                    end;
                    if L24.get(L729[L730][4]) == "off" then
                        L716 = L716 and (L733 ~= L729[L730][5] and L733 ~= L729[L730][6] and L733 ~= L729[L730][7])
                    end;
                    if L24.get(L729[L730][6]) == "off" then
                        L716 = L716 and L733 ~= L729[L730][7]
                    end;
                    if L24.get(L729[L730][8]) then
                        if L24.get(L729[L730][8]) == "off" then
                            L716 = L716 and L733 ~= L729[L730][10]
                        end;
                        if L24.get(L729[L730][8]) == "off" or L24.get(L729[L730][8]) == "opposite" then
                            L716 = L716 and L733 ~= L729[L730][9]
                        end
                    end;
                    if L24.get(L729[L730][6]) == "slow" then
                        L716 = L716 and (L733 ~= L729[L730][9] and L733 ~= L729[L730][8])
                    end
                end;
                L24.set_visible(L733, L716)
            end
        end
    end
end;
writefile(L13("!default_preset2124089493w.cfg"), "dHJ1ZV9taW5pbWFsXzBfYXQgdGFyZ2V0c18xODBfMF9za2l0dGVyXzIwX2ppdHRlcl8wX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfZmFsc2Vfb2ZmX29mZl90cnVlX21pbmltYWxfMF9hdCB0YXJnZXRzXzE4MF8wX3NraXR0ZXJfMzBfaml0dGVyXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX3RydWVfZGVmYXVsdF8wX2F0IHRhcmdldHNfMTgwXzBfc2xvd183MF9qaXR0ZXJfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9kZWZhdWx0XzBfYXQgdGFyZ2V0c18xODBfMF9za2l0dGVyXzUwX2ppdHRlcl8wX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfZmFsc2Vfb2ZmX29mZl90cnVlX2RlZmF1bHRfMF9hdCB0YXJnZXRzXzE4MF8wX3NraXR0ZXJfMzBfaml0dGVyXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX3RydWVfZGVmYXVsdF8wX2F0IHRhcmdldHNfMTgwXzBfc2xvd183M19qaXR0ZXJfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9taW5pbWFsXzBfYXQgdGFyZ2V0c18xODBfLTE1X29mZl81X3N0YXRpY18tNTRfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX3RydWVfbWluaW1hbF8wX2F0IHRhcmdldHNfMTgwXzVfc2tpdHRlcl8zMF9qaXR0ZXJfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfZmFsc2Vfb2ZmXzBfbG9jYWwgdmlld19vZmZfMF9vZmZfMF9vZmZfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9taW5pbWFsXzBfYXQgdGFyZ2V0c18xODBfM19vZmZzZXRfMTlfaml0dGVyXzE4MF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9taW5pbWFsXzBfbG9jYWwgdmlld18xODBfMF9vZmZfMF9zdGF0aWNfMTgwX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfZmFsc2Vfb2ZmX2ppdHRlcl9mYWxzZV91cF8wX2F0IHRhcmdldHNfc3Bpbl8xOV9vZmZfNDdfaml0dGVyXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV91cF9vZmZfdHJ1ZV9yYW5kb21fMF9hdCB0YXJnZXRzXzE4MF8xODBfb2ZmXzBfb2ZmXzE4MF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9taW5pbWFsXzBfYXQgdGFyZ2V0c18xODBfMF9vZmZfOF9zdGF0aWNfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9kZWZhdWx0XzBfYXQgdGFyZ2V0c18xODBfMF9vZmZfMF9zdGF0aWNfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9vZmZfMF9sb2NhbCB2aWV3XzE4MF8xODBfb2ZmXzBfaml0dGVyXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX3RydWVfb2ZmX29mZl8wX29mZl8=")
writefile(L13("!default_fs_preset2124089493w.cfg"), "ZmFsc2Vfb2ZmXzBfbG9jYWwgdmlld19vZmZfMF9vZmZfMF9vZmZfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9kb3duXzBfYXQgdGFyZ2V0c18xODBfMF9za2l0dGVyXzQ1X2ppdHRlcl8wX2ZhbHNlX2ZhbHNlX3RydWVfMF9mYWxzZV9vZmZfb2ZmX3RydWVfZG93bl8wX2F0IHRhcmdldHNfMTgwXy0xX3Nsb3dfNDlfaml0dGVyXzBfZmFsc2VfZmFsc2VfdHJ1ZV8wX3RydWVfb2ZmX29wcG9zaXRlX3RydWVfZG93bl8wX2F0IHRhcmdldHNfMTgwXzFfc2xvd18xMTBfb3Bwb3NpdGVfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX3RydWVfb2ZmX29wcG9zaXRlX3RydWVfZG93bl8wX2F0IHRhcmdldHNfMTgwXy01X2NlbnRlcl8yN19vcHBvc2l0ZV8wX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfdHJ1ZV96ZXJvX3NwaW5fdHJ1ZV9taW5pbWFsXy00Nl9hdCB0YXJnZXRzXzE4MF8tNV9jZW50ZXJfMjdfc3RhdGljXzdfZmFsc2VfZmFsc2VfZmFsc2VfMF90cnVlX3JhbmRvbV9qaXR0ZXJfdHJ1ZV9kb3duXzBfYXQgdGFyZ2V0c18xODBfLTdfb2ZmXzMyX3N0YXRpY18tMTgwX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfZmFsc2Vfb2ZmX29mZl90cnVlX21pbmltYWxfMF9hdCB0YXJnZXRzXzE4MF8tMV9zbG93XzQ1X29wcG9zaXRlXy0xODBfZmFsc2VfZmFsc2VfZmFsc2VfMF90cnVlX21pbmltYWxfb3Bwb3NpdGVfdHJ1ZV9kb3duXzBfYXQgdGFyZ2V0c18xODBfLTJfY2VudGVyXzMyX3N0YXRpY18tMTgwX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfdHJ1ZV9taW5pbWFsX29wcG9zaXRlX2ZhbHNlX29mZl8wX2xvY2FsIHZpZXdfb2ZmXzBfb2ZmXzBfb2ZmXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX2ZhbHNlX29mZl8wX2xvY2FsIHZpZXdfb2ZmXzBfb2ZmXzBfb2ZmXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX3RydWVfZG93bl8wX2F0IHRhcmdldHNfMTgwXzBfb2ZmXzE1X29wcG9zaXRlXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX3RydWVfb2ZmXzBfYXQgdGFyZ2V0c18xODBfMTgwX29mZl8wX29wcG9zaXRlXzBfZmFsc2VfZmFsc2VfZmFsc2VfMF9mYWxzZV9vZmZfb2ZmX2ZhbHNlX21pbmltYWxfMF9hdCB0YXJnZXRzXzE4MF8tMV9vZmZfOF9vcHBvc2l0ZV8zX2ZhbHNlX2ZhbHNlX2ZhbHNlXzBfZmFsc2VfbWluaW1hbF9vZmZfZmFsc2Vfb2ZmXzBfbG9jYWwgdmlld19vZmZfMF9vZmZfMF9vZmZfMF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfdHJ1ZV9jdXN0b21fMF9hdCB0YXJnZXRzX29mZl8wX29mZl8wX29wcG9zaXRlXzE4MF9mYWxzZV9mYWxzZV9mYWxzZV8wX2ZhbHNlX29mZl9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX2Zha2UgZG93biAoLTE4MClfY2VudGVyXzIzX2ppdHRlcl9mYWxzZV9vZmZfb2ZmXzBfb2ZmX2ZhbHNlX29mZl9vZmZfMF9vZmZfZmFsc2Vfb2ZmX29mZl8wX29mZl90cnVlX29mZl9vZmZfMF9vZmZf")
local L735 = function()
    if L24.get(L90["config"][2]) == "" then
        if L132(L24.get(L90["misc"][2]), "config changes") then
            g_notify:add("(error) empty config name", nil, 5)
        end;
        return
    end;
    if not L132(L53(), L24.get(L90["config"][2]) .. "2124089493w.cfg") then
        if L132(L24.get(L90["misc"][2]), "config changes") then
            g_notify:add("'" .. L24.get(L90["config"][2]) .. "' anti-aim config created", nil, 5)
        end;
        writefile(L13(L24.get(L90["config"][2]) .. "2124089493w.cfg"), "blank")
    else
        if L132(L24.get(L90["misc"][2]), "config changes") then
            g_notify:add("(error) '" .. L22.sub(L53()[L24.get(L90["config"][1]) + 1], 1, -16) .. "' anti-aim config already exists", nil, 5)
        end
    end
end;
local L744 = function()
    if L24.get(L90["config"][1]) == nil or L53()[L24.get(L90["config"][1]) + 1] == nil then
        if L132(L24.get(L90["misc"][2]), "config changes") then
            g_notify:add("(error) no config selected", nil, 5)
        end;
        return
    end;
    if readfile(L53()[L24.get(L90["config"][1]) + 1]) == "blank" then
        if L132(L24.get(L90["misc"][2]), "config changes") then
            g_notify:add("(error) '" .. L22.sub(L53()[L24.get(L90["config"][1]) + 1], 1, -16) .. "' anti-aim config is blank", nil, 5)
        end;
        return
    end;
    local L736 = L102(L5.decode(readfile(L53()[L24.get(L90["config"][1]) + 1]), "base64"), "_")
    local L737 = 1;
    for L738, L739 in L9({ L82, L83 }) do
        for L740, L741 in L10(L739) do
            if L739 == L82 then
                for L742 = 0, 16 do
                    if L736[L737] == "true" then
                        L24.set(L739[L740][L742], true)
                    elseif L736[L737] == "false" then
                        L24.set(L739[L740][L742], false)
                    else
                        L24.set(L739[L740][L742], L13(L736[L737]))
                    end;
                    L737 = L737 + 1
                end
            else
                for L743 = 0, 4 do
                    if L736[L737] == "true" then
                        L24.set(L739[L740][L743], true)
                    elseif L736[L737] == "false" then
                        L24.set(L739[L740][L743], false)
                    else
                        L24.set(L739[L740][L743], L13(L736[L737]))
                    end;
                    L737 = L737 + 1
                end
            end
        end
    end;
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("'" .. L22.sub(L53()[L24.get(L90["config"][1]) + 1], 1, -16) .. "' anti-aim config loaded", nil, 5)
    end
end;
local L752 = function()
    local L745 = ""
    for L746, L747 in L9({ L82, L83 }) do
        for L748, L749 in L10(L747) do
            if L747 == L82 then
                for L750 = 0, 16 do
                    L745 = L745 .. L13(L24.get(L747[L748][L750])) .. "_"
                end
            elseif L747 == L83 then
                for L751 = 0, 4 do
                    L745 = L745 .. L13(L24.get(L747[L748][L751])) .. "_"
                end
            end
        end
    end;
    L20.write("current_clip_board_to_save", L5.encode(L745, "base64"))
    read_data = L20.read("current_clip_board_to_save")
    writefile(L53()[L24.get(L90["config"][1]) + 1], read_data)
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("'" .. L22.sub(L53()[L24.get(L90["config"][1]) + 1], 1, -16) .. "' anti-aim config saved", nil, 5)
    end
end;
local L753 = function()
    if L24.get(L90["config"][1]) == nil or L53()[L24.get(L90["config"][1]) + 1] == nil then
        return
    end;
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("'" .. L22.sub(L53()[L24.get(L90["config"][1]) + 1], 1, -16) .. "' anti-aim config deleted", nil, 5)
    end;
    L34.remove_file(L52 .. "/" .. L53()[L24.get(L90["config"][1]) + 1], L53()[L24.get(L90["config"][1]) + 1])
end;
local L756 = function()
    if L80 == nil then
        return
    end;
    for L754, L755 in L10(L84) do
        L24.set(L80[L754][0], false)
        L24.set(L80[L754][1], "off")
        L24.set(L80[L754][2], 0)
        L24.set(L80[L754][3], "local view")
        L24.set(L80[L754][4], "off")
        L24.set(L80[L754][5], 0)
        L24.set(L80[L754][6], "off")
        L24.set(L80[L754][7], 0)
        L24.set(L80[L754][8], "off")
        L24.set(L80[L754][9], 0)
        L24.set(L80[L754][10], false)
        L24.set(L80[L754][11], false)
        L24.set(L80[L754][12], false)
        L24.set(L80[L754][13], 0)
        L24.set(L80[L754][14], false)
        L24.set(L80[L754][15], "off")
        L24.set(L80[L754][16], "off")
    end;
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("anti-aim config reset", nil, 5)
    end
end;
local L765 = function()
    local L757 = L102(L5.decode(L6.get(), "base64"), "_")
    local L758 = 1;
    for L759, L760 in L9({ L82, L83 }) do
        for L761, L762 in L10(L760) do
            if L760 == L82 then
                for L763 = 0, 16 do
                    if L757[L758] == "true" then
                        L24.set(L760[L761][L763], true)
                    elseif L757[L758] == "false" then
                        L24.set(L760[L761][L763], false)
                    else
                        L24.set(L760[L761][L763], L13(L757[L758]))
                    end;
                    L758 = L758 + 1
                end
            else
                for L764 = 0, 4 do
                    if L757[L758] == "true" then
                        L24.set(L760[L761][L764], true)
                    elseif L757[L758] == "false" then
                        L24.set(L760[L761][L764], false)
                    else
                        L24.set(L760[L761][L764], L13(L757[L758]))
                    end;
                    L758 = L758 + 1
                end
            end
        end
    end;
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("imported idealyaw anti-aim", nil, 5)
    end
end;
local L773 = function()
    local L766 = ""
    for L767, L768 in L9({ L82, L83 }) do
        for L769, L770 in L10(L768) do
            if L768 == L82 then
                for L771 = 0, 16 do
                    L766 = L766 .. L13(L24.get(L768[L769][L771])) .. "_"
                end
            elseif L768 == L83 then
                for L772 = 0, 4 do
                    L766 = L766 .. L13(L24.get(L768[L769][L772])) .. "_"
                end
            end
        end
    end;
    L6.set(L5.encode(L766), "base64")
    if L132(L24.get(L90["misc"][2]), "config changes") then
        g_notify:add("exported idealyaw anti-aim", nil, 5)
    end
end;
L90["config"][9] = L24.new_button("AA", "Anti-aimbot angles", "create", L735)
L90["config"][3] = L24.new_button("AA", "Anti-aimbot angles", "load", L744)
L90["config"][4] = L24.new_button("AA", "Anti-aimbot angles", "save", L752)
L90["config"][5] = L24.new_button("AA", "Anti-aimbot angles", "delete", L753)
L90["config"][6] = L24.new_button("AA", "Anti-aimbot angles", "reset", L756)
L90["config"][7] = L24.new_button("AA", "Anti-aimbot angles", "import from clipboard", L765)
L90["config"][8] = L24.new_button("AA", "Anti-aimbot angles", "export to clipboard", L773)
local L777 = function()
    L148()
    L154(false)
    L24.set_visible(L127.plist.force_body, true)
    L24.set_visible(L127.plist.force_body_value, true)
    local L774 = L27.get_players(true)
    if #L774 == 0 then
        return nil
    end;
    for L775, L776 in L9(L774) do
        L18.set(L776, "Force body yaw", false)
        L18.set(L776, "Force body yaw value", 0)
    end
end;
local L781 = function(L778)
    local L779 = L24.get(L778)
    local L780 = L779 and L28.set_event_callback or L28.unset_event_callback;
    L780("paint", L460)
    L780("pre_render", L493)
    L780("run_command", L498)
    L780("predict_command", L501)
    L780("setup_command", L619)
    L780("net_update_start", L629)
    L780("net_update_end", L674)
    L780("dormant_hit", L521)
    L780("dormant_miss", L523)
    L780("round_prestart", L506)
    L780("aim_fire", L512)
    L780("player_hurt", L518)
    L780("aim_miss", L520)
    L780("player_death", L441)
    L780("bomb_defused", function()
        L70.bomb_defused = true
    end)
    L780("bomb_exploded", function()
        L70.bomb_exploded = true
    end)
    L780("cs_match_end_restart", reset)
    L780("cs_game_disconnected", reset)
    L780("client_disconnect", reset)
    L780("player_connect_full", reset)
    L780("game_newmap", reset)
end;
L24.set_callback(L76, L781)
L781(L76)
L28.set_event_callback("paint_ui", L734)
L28.set_event_callback("shutdown", L777)
cvar.cl_use_opens_buy_menu:set_int(0)
cvar.cl_autowepswitch:set_int(0)


-- Declare globals once at the top
local last_shot_data = {}
local shot_counter = 0

-- Aim fire callback to track shots
client.set_event_callback("aim_fire", function(e)
    if not e.target then return end

    shot_counter = shot_counter + 1

    last_shot_data[e.target] = {
        hitchance = math.floor(e.hit_chance or 0),
        tick = globals.tickcount(),
        safepoint = e.safepoint or 1, 
        id = shot_counter
    }
end)

-- Declare globals once at the top
local last_shot_data = {}
local shot_counter = 0

-- Aim fire callback to track shots
client.set_event_callback("aim_fire", function(e)
    if not e.target then return end

    shot_counter = shot_counter + 1

    last_shot_data[e.target] = {
        hitchance = math.floor(e.hit_chance or 0),
        tick = globals.tickcount(),
        safepoint = e.safepoint or 1, 
        id = shot_counter
    }
end)

-- Player hurt callback to log hits
client.set_event_callback("player_hurt", function(e)
    local local_player = entity.get_local_player()
    local attacker = client.userid_to_entindex(e.attacker)
    local victim = client.userid_to_entindex(e.userid)

    if attacker ~= local_player then return end

    local name = entity.get_player_name(victim)
    local dmg = e.dmg_health
    local remaining = e.health
    local hitbox = e.hitgroup
    local weapon = e.weapon or ""

    local hitgroup_names = {
        [1] = "head", [2] = "chest", [3] = "stomach",
        [4] = "left arm", [5] = "right arm", [6] = "left leg", [7] = "right leg"
    }

    local hitgroup_name = hitgroup_names[hitbox] or "generic"

    local simtime = entity.get_prop(victim, "m_flSimulationTime") or 0
    local bt = globals.curtime() - simtime

    if bt > 1.0 then
        bt = 0
    end

    local shot_info = last_shot_data[victim] or {}
    local hc = shot_info.hitchance or 0
    local sp = shot_info.safepoint or 1  
    local id = shot_info.id or 0

    local prefix = (weapon == "inferno") and "Burned" or "Hit"

    client.color_log(173, 255, 47, "[ideal yaw] ")
    client.color_log(255, 255, 255, string.format("[%d] %s %s's %s for %d (%d remaining) [bt: %.2f | hc: %d%% | sp: %d]", id, prefix, name, hitgroup_name, dmg, remaining, bt, hc, sp))
end)



--==[ idealyaw_flag.lua ]==--

local images = require "gamesense/images"

local svg_person = images.load_svg([[
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 9 6" width="900" height="600"><rect fill="#fff" width="9" height="3"/><rect fill="#d52b1e" y="3" width="9" height="3"/><rect fill="#0039a6" y="2" width="9" height="2"/></svg>
]])




local cp_color  = ui.new_color_picker("LUA", "A", "Person Color", 255, 255, 255, 255)


client.set_event_callback("paint_ui", function()

    local r, g, b, a = 255, 255, 255, 255
    local x = 11
    local y = 556
    local size = 23

    if svg_person then
        svg_person:draw(x, y, nil, size, r, g, b, a)
    end
end)


--==[ idealyaw_gradient.lua ]==--
local ui_new_checkbox = ui.new_checkbox
local ui_new_slider = ui.new_slider
local ui_new_color_picker = ui.new_color_picker
local ui_get = ui.get
local renderer_rectangle = renderer.rectangle


client.set_event_callback("paint_ui", function()
   

    local r, g, b, a = 205, 123, 123, 255
    local width = 113
    local height = 32
    local x0 = 7
    local y0 = 552

    for i = 0, width - 1 do
        local alpha = a * (1 - i / width)
        renderer_rectangle(x0 + i, y0, 1, height, r, g, b, alpha)
    end
end)


--==[ idealyaw_hc.lua ]==--
-- Переменные
local last_shot_data = {}
local shot_counter = 0
local last_dmg = 0
local last_hc = 0
local last_ratio = 0
local last_id = 0

-- Генерация значений с контролем разницы
local function generate_values()
    local dmg = math.random(40, 126)
    local hc_min = dmg + 1
    local hc_max = math.min(dmg + 50, 200)
    local hc = math.random(hc_min, hc_max)
    local ratio = (dmg / hc) * 100
    return dmg, hc, ratio
end

-- aim_fire: сохраняем значения на выстрел
client.set_event_callback("aim_fire", function(e)
    if not e.target then return end

    shot_counter = shot_counter + 1
    local dmg, hc, ratio = generate_values()

    last_shot_data[e.target] = {
        dmg = dmg,
        hc = hc,
        ratio = ratio,
        id = shot_counter
    }
end)

-- player_hurt: при попадании обновляем финальные значения
client.set_event_callback("player_hurt", function(e)
    local lp = entity.get_local_player()
    local attacker = client.userid_to_entindex(e.attacker)
    local victim = client.userid_to_entindex(e.userid)

    if attacker ~= lp then return end

    local info = last_shot_data[victim] or {}
    if (info.id or 0) > last_id then
        last_dmg = info.dmg or 0
        last_hc = info.hc or 0
        last_ratio = info.ratio or 0
        last_id = info.id
    end
end)

-- paint_ui: отрисовка текста с RGB и возможностью менять размер
client.set_event_callback("paint_ui", function()
    local x = - 27
    local y = 560
    local textX = x + 35

    -- Настройки для RGB и размера текста
    local r, g, b = 255, 255, 255  -- Белый цвет, можно менять на любые RGB значения
    local font_size = 799 -- Размер текста (можно изменять для увеличения или уменьшения)

    -- Формируем строку для отображения данных
    local text = string.format("%d / %d (%.1f)", last_dmg, last_hc, last_ratio)

    -- Отрисовка текста с цветом и размером
    renderer.text(textX, y + 28, r, g, b, 255, "b", font_size, text) 
end)


--==[ idealyaw_name.lua ]==--




client.set_event_callback("paint_ui", function()
    
    local x_pos = 11  
    local y_pos = 556 


    local text_x = x_pos + 35 
    
    
    local r, g, b, a = 255, 255, 255, 255  -- Белый цвет для "IDEALYAW"
    local debug_r, debug_g, debug_b, debug_a = 195, 114, 114, 255  -- Цвет для "[DEBUG]"
    local user_r, user_g, user_b, user_a = 255, 255, 255, 255  -- Белый цвет для "USER:M0R4N0"

    
    renderer.text(text_x, y_pos, r, g, b, a, "-", 0, "IDEALYAW")
    renderer.text(text_x + 36, y_pos, debug_r, debug_g, debug_b, debug_a, "-", 0, "[DEBUG]")
    renderer.text(text_x, y_pos + 14, user_r, user_g, user_b, user_a, "-", 0, "USER:M0R4N0")
end)


--==[ idealyaw_tsi.lua ]==--
local slow, key = ui.reference("aa", "other", "slow motion")
local limitfl = ui.reference("aa", "fake lag", "limit")

local z = {}
z.items = {
    keys = {
        dt = {ui.reference("rage", "aimbot", "double tap")},
        mode = select(2, ui.reference("rage", "aimbot", "double tap")),
        hs = {ui.reference("aa", "other", "on shot anti-aim")},
        fd = {ui.reference("rage", "other", "duck peek assist")},
        sp = {ui.reference("rage", "aimbot", "force safe point")},
        fb = {ui.reference("rage", "aimbot", "force body aim")},
    }
}

z.menu = {
    ["Keybinds"] = {
        left = ui.new_hotkey("aa", "anti-aimbot angles", "Left"),
        right = ui.new_hotkey("aa", "anti-aimbot angles", "Right"),
        forward = ui.new_hotkey("aa", "anti-aimbot angles", "Forward"),
        fs = ui.new_hotkey("aa", "anti-aimbot angles", "Freestand")
    },
    ["Visuals"] = {
        arrows = ui.new_checkbox("aa", "anti-aimbot angles", "Arrows"),
        keys = ui.new_combobox("aa", "anti-aimbot angles", "\nArrows", {"b", " ", "+", "ts", "best"}),
        keycolor = ui.new_color_picker("aa", "anti-aimbot angles", "Key Color", 55, 55, 55, 255),
        colorkey = ui.new_color_picker("aa", "anti-aimbot angles", "Color Key", 179, 255, 18, 255)
    }
}

z.cache = {
    manual = {
        aa = 0,
        tick = 0
    }
}

function z.indicator()
    if not entity.is_alive(entity.get_local_player()) then return end
    if not ui.get(z.menu["Visuals"].arrows) then return end

    local w, h = client.screen_size()
    w = w / 2
    h = h / 2

    local leftkey = "<"
    local rightkey = ">"
    local style = ui.get(z.menu["Visuals"].keys)

    local r, g, b, a = ui.get(z.menu["Visuals"].keycolor)
    local rr, gg, bb = ui.get(z.menu["Visuals"].colorkey)

    if style == "ts" then
        leftkey = "⯇"
        rightkey = "⯈"
        style = "+"
        local yaw_body = math.max(-60, math.min(60, math.floor((entity.get_prop(entity.get_local_player(), "m_flPoseParameter", 11) or 0) * 120 - 60 + 0.5)))
        renderer.line(w - 42, h-8, w - 42, h+8, rr, gg, bb, yaw_body > 0 and 55 or 255)
        renderer.line(w + 42, h-8, w + 42, h+8, rr, gg, bb, yaw_body < 0 and 255 or 55)
        h = h - 2.5
    elseif style == "best" then
        leftkey = "⮜"
        rightkey = "⮞"
        style = "b"
    end

    local manual = z.cache.manual.aa

    if manual == -90 then
        renderer.text(w - 50, h, rr, gg, bb, 255, "c" .. style, 0, leftkey)
    else
        renderer.text(w - 50, h, r, g, b, a, "c" .. style, 0, leftkey)
    end

    if manual == 90 then
        renderer.text(w + 50, h, rr, gg, bb, 255, "c" .. style, 0, rightkey)
    else
        renderer.text(w + 50, h, r, g, b, a, "c" .. style, 0, rightkey)
    end
end

client.set_event_callback("paint", z.indicator)

client.set_event_callback("run_command", function()
    local tick = globals.tickcount()

    if ui.get(z.menu["Keybinds"].left) and z.cache.manual.tick < tick - 11 then
        z.cache.manual.aa = (z.cache.manual.aa == -90) and 0 or -90
        z.cache.manual.tick = tick
    end

    if ui.get(z.menu["Keybinds"].right) and z.cache.manual.tick < tick - 11 then
        z.cache.manual.aa = (z.cache.manual.aa == 90) and 0 or 90
        z.cache.manual.tick = tick
    end

    if ui.get(z.menu["Keybinds"].forward) and z.cache.manual.tick < tick - 11 then
        z.cache.manual.aa = (z.cache.manual.aa == 180) and 0 or 180
        z.cache.manual.tick = tick
    end
end)

return z


--==[ idealyaw_ui.lua ]==--
-- local variables for API functions. any changes to the line below will be lost on re-generation
local bit_band, bit_lshift, client_color_log, client_create_interface, client_delay_call, client_find_signature, client_key_state, client_reload_active_scripts, client_screen_size, client_set_event_callback, client_system_time, client_timestamp, client_unset_event_callback, database_read, database_write, entity_get_classname, entity_get_local_player, entity_get_origin, entity_get_player_name, entity_get_prop, entity_get_steam64, entity_is_alive, globals_framecount, globals_realtime, math_ceil, math_floor, math_max, math_min, panorama_loadstring, renderer_gradient, renderer_line, renderer_rectangle, table_concat, table_insert, table_remove, table_sort, ui_get, ui_is_menu_open, ui_mouse_position, ui_new_checkbox, ui_new_color_picker, ui_new_combobox, ui_new_slider, ui_set, ui_set_visible, setmetatable, pairs, error, globals_absoluteframetime, globals_curtime, globals_frametime, globals_maxplayers, globals_tickcount, globals_tickinterval, math_abs, type, pcall, renderer_circle_outline, renderer_load_rgba, renderer_measure_text, renderer_text, renderer_texture, tostring, ui_name, ui_new_button, ui_new_hotkey, ui_new_label, ui_new_listbox, ui_new_textbox, ui_reference, ui_set_callback, ui_update, unpack, tonumber = bit.band, bit.lshift, client.color_log, client.create_interface, client.delay_call, client.find_signature, client.key_state, client.reload_active_scripts, client.screen_size, client.set_event_callback, client.system_time, client.timestamp, client.unset_event_callback, database.read, database.write, entity.get_classname, entity.get_local_player, entity.get_origin, entity.get_player_name, entity.get_prop, entity.get_steam64, entity.is_alive, globals.framecount, globals.realtime, math.ceil, math.floor, math.max, math.min, panorama.loadstring, renderer.gradient, renderer.line, renderer.rectangle, table.concat, table.insert, table.remove, table.sort, ui.get, ui.is_menu_open, ui.mouse_position, ui.new_checkbox, ui.new_color_picker, ui.new_combobox, ui.new_slider, ui.set, ui.set_visible, setmetatable, pairs, error, globals.absoluteframetime, globals.curtime, globals.frametime, globals.maxplayers, globals.tickcount, globals.tickinterval, math.abs, type, pcall, renderer.circle_outline, renderer.load_rgba, renderer.measure_text, renderer.text, renderer.texture, tostring, ui.name, ui.new_button, ui.new_hotkey, ui.new_label, ui.new_listbox, ui.new_textbox, ui.reference, ui.set_callback, ui.update, unpack, tonumber

local ffi = require 'ffi'
local vector = require 'vector'
local images = require 'gamesense/images'
local anti_aim = require 'gamesense/antiaim_funcs'

local icon = renderer.load_svg([[<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="501px" height="498px" style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd" xmlns:xlink="http://www.w3.org/1999/xlink">
<g><path style="opacity:0.999" fill="#fefefe" d="M 392.5,3.5 C 391.448,3.35055 390.448,3.51722 389.5,4C 391.679,4.44185 392.345,5.44185 391.5,7C 394.353,9.59556 397.686,11.4289 401.5,12.5C 403.167,14.8333 405.167,16.8333 407.5,18.5C 409.268,20.9389 410.601,23.6056 411.5,26.5C 412.672,26.9186 413.672,27.5853 414.5,28.5C 415.439,32.4643 416.272,36.4643 417,40.5C 418.333,41.8333 419.667,43.1667 421,44.5C 422.481,43.5291 423.315,42.1958 423.5,40.5C 424.833,46.1667 424.833,51.8333 423.5,57.5C 423.225,55.1582 422.392,55.1582 421,57.5C 420.667,56.8333 420.333,56.1667 420,55.5C 419.5,56.6667 418.667,57.5 417.5,58C 418.517,59.0495 418.684,60.2161 418,61.5C 416.095,63.4241 414.928,65.7574 414.5,68.5C 413.372,69.2621 412.205,69.9288 411,70.5C 410.644,76.0627 407.811,79.5627 402.5,81C 402.833,81.3333 403.167,81.6667 403.5,82C 401.751,85.5254 399.584,86.0254 397,83.5C 393.623,84.8199 390.123,85.8199 386.5,86.5C 385.208,88.6666 384.375,90.9999 384,93.5C 382.053,112.441 382.219,131.441 384.5,150.5C 383.782,156.84 383.449,163.173 383.5,169.5C 384.484,172.659 386.484,173.659 389.5,172.5C 392.55,174.057 395.717,175.391 399,176.5C 399.667,186.5 399.667,196.5 399,206.5C 398.422,209.847 397.922,213.347 397.5,217C 398.782,221.776 401.116,225.942 404.5,229.5C 403.833,229.833 403.167,230.167 402.5,230.5C 405.131,232.005 404.797,232.671 401.5,232.5C 401.657,233.873 401.49,235.207 401,236.5C 400.667,236.167 400.333,235.833 400,235.5C 399.384,238.787 397.884,241.621 395.5,244C 396.141,247.743 396.141,251.577 395.5,255.5C 396.5,255.5 397.5,255.5 398.5,255.5C 398.939,259.923 398.939,264.256 398.5,268.5C 399.086,273.775 400.086,278.942 401.5,284C 400.806,286.553 399.973,289.053 399,291.5C 398.333,292.833 397.667,292.833 397,291.5C 396.667,292.167 396.333,292.833 396,293.5C 394.667,293.5 393.333,293.5 392,293.5C 391.667,292.833 391.333,292.167 391,291.5C 389,292.833 387,292.833 385,291.5C 383.416,292.861 381.582,293.528 379.5,293.5C 378.625,297.161 378.291,300.661 378.5,304C 378.918,307.35 380.252,310.184 382.5,312.5C 382.287,319.174 381.954,325.841 381.5,332.5C 380.596,333.209 380.263,334.209 380.5,335.5C 379.5,335.5 378.5,335.5 377.5,335.5C 376.352,349.835 376.352,364.168 377.5,378.5C 377.333,381.833 377.167,385.167 377,388.5C 375.539,390.294 375.372,392.294 376.5,394.5C 376.299,398.424 375.799,398.424 375,394.5C 374.919,399.524 375.419,404.524 376.5,409.5C 375.573,416.51 374.573,423.51 373.5,430.5C 374.041,433.208 374.708,435.874 375.5,438.5C 374.185,452.134 374.185,465.8 375.5,479.5C 378.76,480.855 380.427,483.355 380.5,487C 380.801,490.407 380.468,493.907 379.5,497.5C 352.167,497.5 324.833,497.5 297.5,497.5C 296.189,494.878 294.855,492.211 293.5,489.5C 291.898,490.55 291.065,489.883 291,487.5C 290.586,487.957 290.086,488.291 289.5,488.5C 288.526,486.257 288.192,483.924 288.5,481.5C 289.5,481.5 290.5,481.5 291.5,481.5C 291.215,477.975 291.881,474.642 293.5,471.5C 293.392,470.558 293.059,469.725 292.5,469C 294.754,467.946 295.087,466.446 293.5,464.5C 295.611,461.647 295.611,458.981 293.5,456.5C 294.769,452.351 295.435,448.018 295.5,443.5C 295.096,438.656 295.096,433.99 295.5,429.5C 294.605,426.192 293.771,422.859 293,419.5C 291.844,420.993 291.01,420.826 290.5,419C 291.029,417.441 291.696,415.941 292.5,414.5C 291.522,413.199 291.855,412.032 293.5,411C 290.638,406.275 288.305,401.275 286.5,396C 286.318,390.194 286.652,384.528 287.5,379C 287.156,377.635 286.489,376.468 285.5,375.5C 287.062,372.386 286.729,369.553 284.5,367C 285.249,365.266 285.749,363.433 286,361.5C 286.333,362.167 286.667,362.833 287,363.5C 291.057,354.999 292.39,345.999 291,336.5C 289.024,335.572 287.191,334.405 285.5,333C 284.101,332.405 282.768,332.572 281.5,333.5C 279.075,331.855 276.408,330.689 273.5,330C 268.336,324.816 263.836,318.983 260,312.5C 254.64,308.337 250.306,303.337 247,297.5C 246.292,298.381 245.458,299.047 244.5,299.5C 241.969,294.802 238.303,291.302 233.5,289C 233.833,288.667 234.167,288.333 234.5,288C 232.557,288.305 230.557,288.305 228.5,288C 224.877,282.896 220.544,282.23 215.5,286C 218.133,288.913 217.467,290.746 213.5,291.5C 212.399,297.57 210.232,303.237 207,308.5C 205.921,310.394 204.587,310.727 203,309.5C 202.333,311.167 202.333,312.833 203,314.5C 203.893,313.289 204.726,313.289 205.5,314.5C 203.995,315.842 203.328,317.508 203.5,319.5C 202.789,326.298 201.455,332.965 199.5,339.5C 197.086,343.291 193.92,346.291 190,348.5C 189.562,351.376 188.562,354.043 187,356.5C 174.454,366.126 169.788,378.792 173,394.5C 169.453,402.308 165.619,409.975 161.5,417.5C 160.095,422.878 158.595,428.211 157,433.5C 153.71,438.158 149.71,442.158 145,445.5C 139.683,456.741 137.85,468.407 139.5,480.5C 139.343,481.873 139.51,483.207 140,484.5C 140.21,482.942 140.71,481.609 141.5,480.5C 142.167,486.167 142.833,491.833 143.5,497.5C 124.833,497.5 106.167,497.5 87.5,497.5C 87.1758,493.445 87.5091,489.445 88.5,485.5C 91.5461,475.204 94.5461,465.038 97.5,455C 97.0426,454.586 96.7093,454.086 96.5,453.5C 99.4608,446.916 99.9608,440.25 98,433.5C 97.5357,434.094 97.369,434.761 97.5,435.5C 96.596,434.791 96.2627,433.791 96.5,432.5C 96.5905,419.537 100.257,407.704 107.5,397C 108.852,390.873 110.018,384.706 111,378.5C 113.075,374.1 115.408,369.433 118,364.5C 118.333,364.833 118.667,365.167 119,365.5C 122.556,359.43 125.556,353.43 128,347.5C 129.543,345.622 131.376,344.122 133.5,343C 132.577,340.952 133.077,339.119 135,337.5C 135.752,333.163 136.086,328.829 136,324.5C 135.722,325.416 135.222,326.082 134.5,326.5C 134.175,318.981 134.508,311.648 135.5,304.5C 135.336,307.187 135.503,309.854 136,312.5C 136.333,309.5 136.667,306.5 137,303.5C 139.774,301.511 140.774,298.845 140,295.5C 139.237,298.063 138.737,298.063 138.5,295.5C 138.92,291.774 139.92,288.274 141.5,285C 139.875,282.863 140.208,281.197 142.5,280C 142.235,275.128 142.235,269.962 142.5,264.5C 140.536,261.982 139.87,259.316 140.5,256.5C 139.833,255.833 139.167,255.167 138.5,254.5C 140.967,250.935 141.133,247.268 139,243.5C 138.667,243.833 138.333,244.167 138,244.5C 136.904,238.087 137.904,232.087 141,226.5C 142.542,224.696 144.209,223.029 146,221.5C 146.35,212.906 145.85,204.572 144.5,196.5C 144.39,194.626 145.056,193.126 146.5,192C 146.167,191.667 145.833,191.333 145.5,191C 147.968,185.96 150.635,180.96 153.5,176C 153.167,175.667 152.833,175.333 152.5,175C 154.187,173.087 154.687,170.92 154,168.5C 151.929,167.636 150.262,166.303 149,164.5C 148.667,164.833 148.333,165.167 148,165.5C 147.365,164.034 146.531,162.7 145.5,161.5C 146.025,160.808 146.692,160.308 147.5,160C 146.422,159.326 145.755,158.326 145.5,157C 146.123,153.519 146.623,150.019 147,146.5C 148.791,142.589 150.291,138.589 151.5,134.5C 155.71,122.129 162.543,111.463 172,102.5C 173.613,103.622 174.78,103.122 175.5,101C 177.8,100.342 180.133,99.8417 182.5,99.5C 186.008,100.115 189.341,101.115 192.5,102.5C 194.937,102.402 196.937,101.402 198.5,99.5C 201.143,95.0232 204.643,91.3565 209,88.5C 210.841,84.8168 213.174,81.4835 216,78.5C 216.333,78.8333 216.667,79.1667 217,79.5C 217.36,77.3921 218.027,75.3921 219,73.5C 224.159,67.1831 228.826,60.5165 233,53.5C 237.043,53.4656 239.376,51.1323 240,46.5C 242.705,43.9638 245.205,41.2971 247.5,38.5C 251.358,34.5503 255.691,31.0503 260.5,28C 268.951,23.3032 277.951,19.9699 287.5,18C 294.97,16.2134 301.47,17.7134 307,22.5C 309.498,21.4018 311.998,21.5684 314.5,23C 316.853,26.1024 319.519,28.1024 322.5,29C 324.473,29.4955 326.473,29.6621 328.5,29.5C 328.383,27.5165 329.05,25.8498 330.5,24.5C 335.296,20.5352 339.63,16.0352 343.5,11C 347.429,8.21295 351.429,5.71295 355.5,3.5C 367.98,2.23854 380.314,2.23854 392.5,3.5 Z M 355.5,420.5 C 356.888,427.273 356.555,433.939 354.5,440.5C 353.852,442.086 353.352,443.753 353,445.5C 352.554,442.657 352.054,439.824 351.5,437C 352.302,433.596 353.302,430.263 354.5,427C 354.297,424.594 353.297,422.594 351.5,421C 352.793,420.51 354.127,420.343 355.5,420.5 Z"/></g>
<g><path style="opacity:0.8" fill="#eeedeb" d="M 355.5,3.5 C 351.429,5.71295 347.429,8.21295 343.5,11C 339.63,16.0352 335.296,20.5352 330.5,24.5C 329.05,25.8498 328.383,27.5165 328.5,29.5C 326.473,29.6621 324.473,29.4955 322.5,29C 319.519,28.1024 316.853,26.1024 314.5,23C 311.998,21.5684 309.498,21.4018 307,22.5C 301.47,17.7134 294.97,16.2134 287.5,18C 277.951,19.9699 268.951,23.3032 260.5,28C 255.691,31.0503 251.358,34.5503 247.5,38.5C 247.158,37.6618 246.492,37.3284 245.5,37.5C 262.502,19.9996 283.169,13.1663 307.5,17C 313.96,19.7293 319.96,23.2293 325.5,27.5C 331.284,18.549 338.617,11.049 347.5,5C 350.063,3.92074 352.729,3.42074 355.5,3.5 Z"/></g>
<g><path style="opacity:0.645" fill="#faf9f1" d="M 392.5,3.5 C 400.47,4.40532 406.97,8.07199 412,14.5C 417.732,22.2998 421.565,30.9664 423.5,40.5C 423.315,42.1958 422.481,43.5291 421,44.5C 419.667,43.1667 418.333,41.8333 417,40.5C 416.272,36.4643 415.439,32.4643 414.5,28.5C 413.672,27.5853 412.672,26.9186 411.5,26.5C 410.601,23.6056 409.268,20.9389 407.5,18.5C 405.167,16.8333 403.167,14.8333 401.5,12.5C 397.686,11.4289 394.353,9.59556 391.5,7C 392.345,5.44185 391.679,4.44185 389.5,4C 390.448,3.51722 391.448,3.35055 392.5,3.5 Z"/></g>
<g><path style="opacity:0.898" fill="#eeedf1" d="M 245.5,37.5 C 246.492,37.3284 247.158,37.6618 247.5,38.5C 245.205,41.2971 242.705,43.9638 240,46.5C 239.376,51.1323 237.043,53.4656 233,53.5C 228.826,60.5165 224.159,67.1831 219,73.5C 218.027,75.3921 217.36,77.3921 217,79.5C 216.667,79.1667 216.333,78.8333 216,78.5C 213.174,81.4835 210.841,84.8168 209,88.5C 204.643,91.3565 201.143,95.0232 198.5,99.5C 196.937,101.402 194.937,102.402 192.5,102.5C 189.341,101.115 186.008,100.115 182.5,99.5C 180.133,99.8417 177.8,100.342 175.5,101C 174.78,103.122 173.613,103.622 172,102.5C 162.543,111.463 155.71,122.129 151.5,134.5C 149.126,137.949 147.126,141.616 145.5,145.5C 148.867,127.261 157.534,112.094 171.5,100C 179.308,96.7602 186.975,96.7602 194.5,100C 209.098,82.7384 222.931,64.9051 236,46.5C 239.036,43.2956 242.203,40.2956 245.5,37.5 Z"/></g>
<g><path style="opacity:0.982" fill="#fbfaf4" d="M 423.5,57.5 C 420.556,68.8853 414.89,78.7186 406.5,87C 401.009,90.3728 395.009,91.8728 388.5,91.5C 388.826,100.017 388.493,108.35 387.5,116.5C 387.785,114.712 387.452,113.045 386.5,111.5C 385.334,127.49 385.167,143.49 386,159.5C 386.179,162.553 386.679,165.553 387.5,168.5C 388.298,168.043 388.631,167.376 388.5,166.5C 392.672,168.544 397.005,170.378 401.5,172C 403.074,173.826 403.907,175.993 404,178.5C 404.055,189.841 403.555,201.175 402.5,212.5C 401.888,216.807 403.055,220.474 406,223.5C 408.857,231.602 407.524,238.935 402,245.5C 401.833,247 401.667,248.5 401.5,250C 403.932,263.081 405.099,276.247 405,289.5C 403.895,292.937 401.728,295.437 398.5,297C 394.167,297.333 389.833,297.667 385.5,298C 385,298.5 384.5,299 384,299.5C 382.805,303.751 382.305,308.085 382.5,312.5C 380.252,310.184 378.918,307.35 378.5,304C 378.291,300.661 378.625,297.161 379.5,293.5C 381.582,293.528 383.416,292.861 385,291.5C 387,292.833 389,292.833 391,291.5C 391.333,292.167 391.667,292.833 392,293.5C 393.333,293.5 394.667,293.5 396,293.5C 396.333,292.833 396.667,292.167 397,291.5C 397.667,292.833 398.333,292.833 399,291.5C 399.973,289.053 400.806,286.553 401.5,284C 400.086,278.942 399.086,273.775 398.5,268.5C 398.939,264.256 398.939,259.923 398.5,255.5C 397.5,255.5 396.5,255.5 395.5,255.5C 396.141,251.577 396.141,247.743 395.5,244C 397.884,241.621 399.384,238.787 400,235.5C 400.333,235.833 400.667,236.167 401,236.5C 401.49,235.207 401.657,233.873 401.5,232.5C 404.797,232.671 405.131,232.005 402.5,230.5C 403.167,230.167 403.833,229.833 404.5,229.5C 401.116,225.942 398.782,221.776 397.5,217C 397.922,213.347 398.422,209.847 399,206.5C 399.667,196.5 399.667,186.5 399,176.5C 395.717,175.391 392.55,174.057 389.5,172.5C 386.484,173.659 384.484,172.659 383.5,169.5C 383.449,163.173 383.782,156.84 384.5,150.5C 382.219,131.441 382.053,112.441 384,93.5C 384.375,90.9999 385.208,88.6666 386.5,86.5C 390.123,85.8199 393.623,84.8199 397,83.5C 399.584,86.0254 401.751,85.5254 403.5,82C 403.167,81.6667 402.833,81.3333 402.5,81C 407.811,79.5627 410.644,76.0627 411,70.5C 412.205,69.9288 413.372,69.2621 414.5,68.5C 414.928,65.7574 416.095,63.4241 418,61.5C 418.684,60.2161 418.517,59.0495 417.5,58C 418.667,57.5 419.5,56.6667 420,55.5C 420.333,56.1667 420.667,56.8333 421,57.5C 422.392,55.1582 423.225,55.1582 423.5,57.5 Z"/></g>
<g><path style="opacity:0.999" fill="#f6f4e8" d="M 387.5,116.5 C 388.186,133.158 388.519,149.824 388.5,166.5C 388.631,167.376 388.298,168.043 387.5,168.5C 386.679,165.553 386.179,162.553 386,159.5C 385.167,143.49 385.334,127.49 386.5,111.5C 387.452,113.045 387.785,114.712 387.5,116.5 Z"/></g>
<g><path style="opacity:0.822" fill="#f2f2f6" d="M 151.5,134.5 C 150.291,138.589 148.791,142.589 147,146.5C 146.623,150.019 146.123,153.519 145.5,157C 145.755,158.326 146.422,159.326 147.5,160C 146.692,160.308 146.025,160.808 145.5,161.5C 146.531,162.7 147.365,164.034 148,165.5C 148.333,165.167 148.667,164.833 149,164.5C 150.262,166.303 151.929,167.636 154,168.5C 154.687,170.92 154.187,173.087 152.5,175C 152.833,175.333 153.167,175.667 153.5,176C 150.635,180.96 147.968,185.96 145.5,191C 145.833,191.333 146.167,191.667 146.5,192C 145.056,193.126 144.39,194.626 144.5,196.5C 145.85,204.572 146.35,212.906 146,221.5C 144.209,223.029 142.542,224.696 141,226.5C 137.904,232.087 136.904,238.087 138,244.5C 138.333,244.167 138.667,243.833 139,243.5C 141.133,247.268 140.967,250.935 138.5,254.5C 139.167,255.167 139.833,255.833 140.5,256.5C 139.87,259.316 140.536,261.982 142.5,264.5C 142.235,269.962 142.235,275.128 142.5,280C 140.208,281.197 139.875,282.863 141.5,285C 139.92,288.274 138.92,291.774 138.5,295.5C 138.737,298.063 139.237,298.063 140,295.5C 140.774,298.845 139.774,301.511 137,303.5C 136.667,306.5 136.333,309.5 136,312.5C 135.503,309.854 135.336,307.187 135.5,304.5C 136.614,293.809 137.947,283.143 139.5,272.5C 136.733,258.302 135.9,243.969 137,229.5C 137.775,225.597 139.775,222.597 143,220.5C 143.638,219.391 144.138,218.225 144.5,217C 142.335,207.526 142.168,198.026 144,188.5C 146.226,182.634 148.726,176.968 151.5,171.5C 148.535,169.365 146.035,166.698 144,163.5C 143.333,158.5 143.333,153.5 144,148.5C 144.232,147.263 144.732,146.263 145.5,145.5C 147.126,141.616 149.126,137.949 151.5,134.5 Z"/></g>
<g><path style="opacity:1" fill="#fafbf5" d="M 343.5,242.5 C 351.925,248.483 354.092,256.15 350,265.5C 348.19,261.207 346.357,256.874 344.5,252.5C 338.255,249.566 337.921,246.233 343.5,242.5 Z"/></g>
<g><path style="opacity:0.999" fill="#fbfbf6" d="M 344.5,305.5 C 344.539,306.583 344.873,307.583 345.5,308.5C 344.975,309.192 344.308,309.692 343.5,310C 344.863,311.945 345.697,314.112 346,316.5C 352.638,310.167 354.138,303 350.5,295C 351.059,294.275 351.392,293.442 351.5,292.5C 350.291,289.535 349.291,286.535 348.5,283.5C 349.552,283.351 350.552,283.517 351.5,284C 352.652,286.149 354.152,287.982 356,289.5C 355.756,299.144 355.589,308.811 355.5,318.5C 352.986,318.754 350.652,319.587 348.5,321C 349.517,322.049 349.684,323.216 349,324.5C 345.268,324.45 341.435,323.783 337.5,322.5C 336.671,316.923 336.671,311.423 337.5,306C 335.541,302.876 333.041,300.376 330,298.5C 329.405,297.101 329.572,295.768 330.5,294.5C 329.833,293.833 329.167,293.167 328.5,292.5C 329.309,290.929 329.643,289.262 329.5,287.5C 328.5,287.5 327.5,287.5 326.5,287.5C 324.499,282.783 322.999,277.783 322,272.5C 320.019,270.641 319.019,268.308 319,265.5C 315.882,262.93 314.715,259.596 315.5,255.5C 313.5,255.167 311.5,254.833 309.5,254.5C 309.969,250.09 308.969,246.09 306.5,242.5C 303.338,240.117 300.672,237.284 298.5,234C 296.913,233.138 295.246,232.471 293.5,232C 294.622,229.522 294.122,227.355 292,225.5C 291.349,220.707 291.849,216.04 293.5,211.5C 296.978,211.184 300.312,211.684 303.5,213C 302.72,214.073 302.887,215.24 304,216.5C 305.693,217.184 307.193,218.184 308.5,219.5C 312.817,219.07 316.984,218.07 321,216.5C 322.876,218.123 324.21,217.79 325,215.5C 325.333,216.167 325.667,216.833 326,217.5C 327,216.5 328,215.5 329,214.5C 329.333,215.167 329.667,215.833 330,216.5C 330.674,215.422 331.674,214.755 333,214.5C 337.628,216.628 341.128,219.961 343.5,224.5C 341.995,225.842 341.328,227.508 341.5,229.5C 340.448,229.649 339.448,229.483 338.5,229C 337.035,226.57 335.702,224.07 334.5,221.5C 333.554,221.013 332.554,220.68 331.5,220.5C 323.008,223.166 314.341,223.999 305.5,223C 303.217,221.129 300.717,219.629 298,218.5C 296.842,218.998 296.009,219.831 295.5,221C 303.096,230.993 310.596,241.16 318,251.5C 326.258,268.43 333.591,285.764 340,303.5C 340.333,303.167 340.667,302.833 341,302.5C 342.155,303.338 343.322,304.338 344.5,305.5 Z"/></g>
<g><path style="opacity:0.575" fill="#f0eeec" d="M 244.5,299.5 C 246.039,301.877 247.373,304.377 248.5,307C 248.272,307.399 247.938,307.565 247.5,307.5C 244.022,303.177 240.688,298.677 237.5,294C 232.454,291.876 227.62,289.376 223,286.5C 214.748,296.243 208.914,307.243 205.5,319.5C 205.062,318.494 204.396,318.494 203.5,319.5C 203.328,317.508 203.995,315.842 205.5,314.5C 204.726,313.289 203.893,313.289 203,314.5C 202.333,312.833 202.333,311.167 203,309.5C 204.587,310.727 205.921,310.394 207,308.5C 210.232,303.237 212.399,297.57 213.5,291.5C 217.467,290.746 218.133,288.913 215.5,286C 220.544,282.23 224.877,282.896 228.5,288C 230.557,288.305 232.557,288.305 234.5,288C 234.167,288.333 233.833,288.667 233.5,289C 238.303,291.302 241.969,294.802 244.5,299.5 Z"/></g>
<g><path style="opacity:1" fill="#f9f9f3" d="M 297.5,497.5 C 294.833,497.5 292.167,497.5 289.5,497.5C 286.194,494.217 284.527,490.217 284.5,485.5C 285.736,475.956 287.903,466.623 291,457.5C 291.667,447.5 291.667,437.5 291,427.5C 282.946,405.462 280.279,382.795 283,359.5C 286.309,352.789 287.142,345.789 285.5,338.5C 280.061,337.142 274.728,335.309 269.5,333C 262.041,324.562 254.707,316.062 247.5,307.5C 247.938,307.565 248.272,307.399 248.5,307C 247.373,304.377 246.039,301.877 244.5,299.5C 245.458,299.047 246.292,298.381 247,297.5C 250.306,303.337 254.64,308.337 260,312.5C 263.836,318.983 268.336,324.816 273.5,330C 276.408,330.689 279.075,331.855 281.5,333.5C 282.768,332.572 284.101,332.405 285.5,333C 287.191,334.405 289.024,335.572 291,336.5C 292.39,345.999 291.057,354.999 287,363.5C 286.667,362.833 286.333,362.167 286,361.5C 285.749,363.433 285.249,365.266 284.5,367C 286.729,369.553 287.062,372.386 285.5,375.5C 286.489,376.468 287.156,377.635 287.5,379C 286.652,384.528 286.318,390.194 286.5,396C 288.305,401.275 290.638,406.275 293.5,411C 291.855,412.032 291.522,413.199 292.5,414.5C 291.696,415.941 291.029,417.441 290.5,419C 291.01,420.826 291.844,420.993 293,419.5C 293.771,422.859 294.605,426.192 295.5,429.5C 295.096,433.99 295.096,438.656 295.5,443.5C 295.435,448.018 294.769,452.351 293.5,456.5C 295.611,458.981 295.611,461.647 293.5,464.5C 295.087,466.446 294.754,467.946 292.5,469C 293.059,469.725 293.392,470.558 293.5,471.5C 291.881,474.642 291.215,477.975 291.5,481.5C 290.5,481.5 289.5,481.5 288.5,481.5C 288.192,483.924 288.526,486.257 289.5,488.5C 290.086,488.291 290.586,487.957 291,487.5C 291.065,489.883 291.898,490.55 293.5,489.5C 294.855,492.211 296.189,494.878 297.5,497.5 Z"/></g>
<g><path style="opacity:0.975" fill="#eeedf2" d="M 96.5,432.5 C 96.3337,425.159 96.5003,417.826 97,410.5C 99.561,404.275 102.561,398.275 106,392.5C 106.63,386.757 107.63,381.09 109,375.5C 116.415,362.335 124.081,349.335 132,336.5C 133.727,333.382 134.561,330.049 134.5,326.5C 135.222,326.082 135.722,325.416 136,324.5C 136.086,328.829 135.752,333.163 135,337.5C 133.077,339.119 132.577,340.952 133.5,343C 131.376,344.122 129.543,345.622 128,347.5C 125.556,353.43 122.556,359.43 119,365.5C 118.667,365.167 118.333,364.833 118,364.5C 115.408,369.433 113.075,374.1 111,378.5C 110.018,384.706 108.852,390.873 107.5,397C 100.257,407.704 96.5905,419.537 96.5,432.5 Z"/></g>
<g><path style="opacity:0.971" fill="#fbfaf4" d="M 381.5,332.5 C 380.854,381.166 380.687,429.833 381,478.5C 384.165,484.411 385.332,490.745 384.5,497.5C 382.833,497.5 381.167,497.5 379.5,497.5C 380.468,493.907 380.801,490.407 380.5,487C 380.427,483.355 378.76,480.855 375.5,479.5C 374.185,465.8 374.185,452.134 375.5,438.5C 374.708,435.874 374.041,433.208 373.5,430.5C 374.573,423.51 375.573,416.51 376.5,409.5C 375.419,404.524 374.919,399.524 375,394.5C 375.799,398.424 376.299,398.424 376.5,394.5C 375.372,392.294 375.539,390.294 377,388.5C 377.167,385.167 377.333,381.833 377.5,378.5C 376.352,364.168 376.352,349.835 377.5,335.5C 378.5,335.5 379.5,335.5 380.5,335.5C 380.263,334.209 380.596,333.209 381.5,332.5 Z"/></g>
<g><path style="opacity:0.545" fill="#e4e2e1" d="M 205.5,319.5 C 206.514,332.309 202.014,342.642 192,350.5C 189.568,356.942 185.568,362.276 180,366.5C 179,368.5 178,370.5 177,372.5C 177.012,380.977 176.012,389.31 174,397.5C 167.306,409.894 161.973,422.894 158,436.5C 145.003,446.011 139.503,458.678 141.5,474.5C 139.72,475.99 139.054,477.99 139.5,480.5C 137.85,468.407 139.683,456.741 145,445.5C 149.71,442.158 153.71,438.158 157,433.5C 158.595,428.211 160.095,422.878 161.5,417.5C 165.619,409.975 169.453,402.308 173,394.5C 169.788,378.792 174.454,366.126 187,356.5C 188.562,354.043 189.562,351.376 190,348.5C 193.92,346.291 197.086,343.291 199.5,339.5C 201.455,332.965 202.789,326.298 203.5,319.5C 204.396,318.494 205.062,318.494 205.5,319.5 Z"/></g>
<g><path style="opacity:0.97" fill="#fbfbf6" d="M 354.5,440.5 C 356.555,433.939 356.888,427.273 355.5,420.5C 355.631,419.761 355.464,419.094 355,418.5C 353.274,419.576 351.441,419.743 349.5,419C 348.167,418 348.167,417 349.5,416C 354.115,415.761 358.615,415.594 363,415.5C 363.433,417.664 362.933,419.664 361.5,421.5C 364.802,429.201 365.469,437.201 363.5,445.5C 358.167,446.167 358.167,446.833 363.5,447.5C 362.189,451.468 360.855,455.468 359.5,459.5C 359.716,461.384 360.383,463.051 361.5,464.5C 360.354,465.719 359.354,467.052 358.5,468.5C 356.291,469.106 354.124,469.773 352,470.5C 351.667,468.5 351.333,466.5 351,464.5C 346.597,464.263 344.43,461.93 344.5,457.5C 342.418,457.528 340.584,456.861 339,455.5C 337.88,448.788 337.38,442.122 337.5,435.5C 337.594,433.311 338.261,431.311 339.5,429.5C 337.626,426.667 336.626,423.833 336.5,421C 339.105,418.661 339.438,416.328 337.5,414C 339.762,413.358 341.929,412.525 344,411.5C 345.022,412.354 345.855,413.354 346.5,414.5C 344.283,419.544 342.283,424.211 340.5,428.5C 341,429.5 341.5,430.5 342,431.5C 342.333,431.167 342.667,430.833 343,430.5C 343.366,437.28 343.532,443.947 343.5,450.5C 347.858,454.196 351.525,458.53 354.5,463.5C 355.451,464.326 356.451,464.492 357.5,464C 357.167,463.667 356.833,463.333 356.5,463C 357.293,459.589 357.793,456.089 358,452.5C 358.333,452.833 358.667,453.167 359,453.5C 359.573,448.385 358.073,444.052 354.5,440.5 Z M 355.5,420.5 C 356.888,427.273 356.555,433.939 354.5,440.5C 353.852,442.086 353.352,443.753 353,445.5C 352.554,442.657 352.054,439.824 351.5,437C 352.302,433.596 353.302,430.263 354.5,427C 354.297,424.594 353.297,422.594 351.5,421C 352.793,420.51 354.127,420.343 355.5,420.5 Z"/></g>
<g><path style="opacity:0.745" fill="#f0eff4" d="M 87.5,497.5 C 86.5,497.5 85.5,497.5 84.5,497.5C 87.0436,480.253 90.8769,463.253 96,446.5C 96.7189,442.855 97.2189,439.188 97.5,435.5C 97.369,434.761 97.5357,434.094 98,433.5C 99.9608,440.25 99.4608,446.916 96.5,453.5C 96.7093,454.086 97.0426,454.586 97.5,455C 94.5461,465.038 91.5461,475.204 88.5,485.5C 87.5091,489.445 87.1758,493.445 87.5,497.5 Z"/></g>
<g><path style="opacity:0.773" fill="#c0c0c5" d="M 141.5,474.5 C 141.5,476.5 141.5,478.5 141.5,480.5C 140.71,481.609 140.21,482.942 140,484.5C 139.51,483.207 139.343,481.873 139.5,480.5C 139.054,477.99 139.72,475.99 141.5,474.5 Z"/></g>
</svg>]])

local dragging_fn = function(name, base_x, base_y) return (function()local a={}local b,c,d,e,f,g,h,i,j,k,l,m,n,o;local p={__index={drag=function(self,...)local q,r=self:get()local s,t=a.drag(q,r,...)if q~=s or r~=t then self:set(s,t)end;return s,t end,set=function(self,q,r)local j,k=client_screen_size()ui_set(self.x_reference,q/j*self.res)ui_set(self.y_reference,r/k*self.res)end,get=function(self)local j,k=client_screen_size()return ui_get(self.x_reference)/self.res*j,ui_get(self.y_reference)/self.res*k end}}function a.new(u,v,w,x)x=x or 10000;local j,k=client_screen_size()local y=ui_new_slider('LUA','A',u..' window position',0,x,v/j*x)local z=ui_new_slider('LUA','A','\n'..u..' window position y',0,x,w/k*x)ui_set_visible(y,false)ui_set_visible(z,false)return setmetatable({name=u,x_reference=y,y_reference=z,res=x},p)end;function a.drag(q,r,A,B,C,D,E)if globals_framecount()~=b then c=ui_is_menu_open()f,g=d,e;d,e=ui_mouse_position()i=h;h=client_key_state(0x01)==true;m=l;l={}o=n;n=false;j,k=client_screen_size()end;if c and i~=nil then if(not i or o)and h and f>q and g>r and f<q+A and g<r+B then n=true;q,r=q+d-f,r+e-g;if not D then q=math_max(0,math_min(j-A,q))r=math_max(0,math_min(k-B,r))end end end;table_insert(l,{q,r,A,B})return q,r,A,B end;return a end)().new(name, base_x, base_y) end
local graphs = function()local a={}function a:renderer_line(b,c,d)renderer_line(b.x,b.y,c.x,c.y,d.r,d.g,d.b,d.a)end;function a:renderer_rectangle_outlined(b,c,d)renderer_line(b.x,b.y,b.x,c.y,d.r,d.g,d.b,d.a)renderer_line(b.x,b.y,c.x,b.y,d.r,d.g,d.b,d.a)renderer_line(c.x,b.y,c.x,c.y,d.r,d.g,d.b,d.a)renderer_line(b.x,c.y,c.x,c.y,d.r,d.g,d.b,d.a)end;function a:renderer_rectangle_filled(b,c,d)local e=c.x-b.x;local f=c.y-b.y;if e<0 then if f<0 then renderer_rectangle(c.x,c.y,-e,-f,d.r,d.g,d.b,d.a)else renderer_rectangle(c.x,b.y,-e,f,d.r,d.g,d.b,d.a)end else if f<0 then renderer_rectangle(b.x,c.y,e,-f,d.r,d.g,d.b,d.a)else renderer_rectangle(b.x,b.y,e,f,d.r,d.g,d.b,d.a)end end end;function a:renderer_rectangle_outlined(b,c,d)renderer_line(b.x,b.y,b.x,c.y,d.r,d.g,d.b,d.a)renderer_line(b.x,b.y,c.x,b.y,d.r,d.g,d.b,d.a)renderer_line(c.x,b.y,c.x,c.y,d.r,d.g,d.b,d.a)renderer_line(b.x,c.y,c.x,c.y,d.r,d.g,d.b,d.a)end;function a:renderer_rectangle_filled_gradient(b,c,g,h,i)local e=c.x-b.x;local f=c.y-b.y;if e<0 then if f<0 then renderer_gradient(c.x,c.y,-e,-f,g.r,g.g,g.b,g.a,h.r,h.g,h.b,h.a,i)else renderer_gradient(c.x,b.y,-e,f,g.r,g.g,g.b,g.a,h.r,h.g,h.b,h.a,i)end else if f<0 then renderer_gradient(b.x,c.y,e,-f,h.r,h.g,h.b,h.a,g.r,g.g,g.b,g.a,i)else renderer_gradient(b.x,b.y,e,f,h.r,h.g,h.b,h.a,g.r,g.g,g.b,g.a,i)end end end;function a:draw(j,k,l,m,n,o)local p=k;local q=n.clr_1;k=0;l=l-p;n.h=n.h-n.thickness;if o then a:renderer_rectangle_outlined({x=n.x,y=n.y},{x=n.x+n.w-1,y=n.y+n.h-1+n.thickness},{r=q[1],g=q[2],b=q[3],a=q[4]})end;if k==l then a:renderer_line({x=n.x,y=n.y+n.h},{x=n.x+n.w,y=n.y+n.h},{r=q[1],g=q[2],b=q[3],a=q[4]})return end;local r=n.w/(m-1)local s=l-k;for t=1,m-1 do local u={(j[t]-p)/s,(j[t+1]-p)/s}local v={{x=n.x+r*(t-1),y=n.y+n.h-n.h*u[1]},{x=n.x+r*t,y=n.y+n.h-n.h*u[2]}}for t=1,n.thickness do a:renderer_line({x=v[1].x,y=v[1].y+t-1},{x=v[2].x,y=v[2].y+t-1},{r=q[1],g=q[2],b=q[3],a=q[4]})end end end;function a:draw_histogram(j,k,l,m,n,o)local p=k;k=0;l=l-p;if o then a:renderer_rectangle_outlined({x=n.x,y=n.y},{x=n.x+n.w-1,y=n.y+n.h-1},{r=255,g=255,b=255,a=255})end;local r=n.w/(m-1)local s=l-k;for t=1,m-1 do local u={(j[t]-p)/s,(j[t+1]-p)/s}local v={{x=math_floor(n.x+r*(t-1)),y=math_floor(n.y+n.h-n.h*u[1])},{x=math_floor(n.x+r*t),y=math_floor(n.y+n.h)},isZero=math_floor(n.y+n.h)==math_floor(n.y+n.h-n.h*u[1])}if n.sDrawBar=="fill"then a:renderer_rectangle_filled({x=v[1].x,y=v[1].y},{x=v[2].x,y=v[2].y},{r=n.clr_1[1],g=n.clr_1[2],b=n.clr_1[3],a=n.clr_1[4]})elseif n.sDrawBar=="gradient_fadeout"then a:renderer_rectangle_filled_gradient({x=v[1].x,y=v[1].y},{x=v[2].x,y=v[2].y},{r=n.clr_1[1],g=n.clr_1[2],b=n.clr_1[3],a=0},{r=n.clr_1[1],g=n.clr_1[2],b=n.clr_1[3],a=n.clr_1[4]},false)elseif n.sDrawBar=="gradient_fadein"then a:renderer_rectangle_filled_gradient({x=v[1].x,y=v[1].y},{x=v[2].x,y=v[2].y},{r=n.clr_1[1],g=n.clr_1[2],b=n.clr_1[3],a=n.clr_1[4]},{r=n.clr_1[1],g=n.clr_1[2],b=n.clr_1[3],a=0},false)else end;if n.bDrawPeeks and not v.isZero then a:renderer_line({x=v[1].x,y=v[1].y},{x=v[2].x,y=v[1].y},{r=n.clr_2[1],g=n.clr_2[2],b=n.clr_2[3],a=n.clr_2[4]})end end end;return a end
local gram_create = function(value, count) local gram = { }; for i=1, count do gram[i] = value; end return gram; end
local gram_update = function(tab, value, forced) local new_tab = tab; if forced or new_tab[#new_tab] ~= value then table_insert(new_tab, value); table_remove(new_tab, 1); end; tab = new_tab; end
local get_average = function(tab) local elements, sum = 0, 0; for k, v in pairs(tab) do sum = sum + v; elements = elements + 1; end return sum / elements; end
local hsv_to_rgb = function(b,c,d,e)local f,g,h;local i=math_floor(b*6)local j=b*6-i;local k=d*(1-c)local l=d*(1-j*c)local m=d*(1-(1-j)*c)i=i%6;if i==0 then f,g,h=d,m,k elseif i==1 then f,g,h=l,d,k elseif i==2 then f,g,h=k,d,m elseif i==3 then f,g,h=k,l,d elseif i==4 then f,g,h=m,k,d elseif i==5 then f,g,h=d,k,l end;return f*255,g*255,h*255,e*255 end
local notes = function(b)local c=function(d,e)local f={}for g in pairs(d)do table_insert(f,g)end;table_sort(f,e)local h=0;local i=function()h=h+1;if f[h]==nil then return nil else return f[h],d[f[h]]end end;return i end;local j={get=function(k)local l,m=0,{}for n,o in c(package.idealyaw_notes)do if o==true then l=l+1;m[#m+1]={n,l}end end;for p=1,#m do if m[p][1]==b then return k(m[p][2]-1)end end end,set_state=function(q)package.idealyaw_notes[b]=q;table_sort(package.idealyaw_notes)end,unset=function()client_unset_event_callback('shutdown',callback)end}client_set_event_callback('shutdown',function()if package.idealyaw_notes[b]~=nil then package.idealyaw_notes[b]=nil end end)if package.idealyaw_notes==nil then package.idealyaw_notes={}end;return j end
local item_count = function(b)if b==nil then return 0 end;if#b==0 then local c=0;for d in pairs(b)do c=c+1 end;return c end;return#b end
local contains = function(b,c)for d=1,#b do if b[d]==c then return true end end;return false end
local create_integer = function(b,c,d,e)return{min=b,max=c,init_val=d,scale=e,value=d}end


local read_database = function(script_name, db_name, original)
	if (script_name == nil or script_name == '') or (db_name == nil or db_name == '') or (original == nil or original == { }) then
		client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
		client_color_log(255, 0, 0, 'Error occured while parsing data')
		
		error()
	end

	local dbase = database_read(db_name)
	local new_data, corrupted_data, missing_sectors =
		false, false, { }

	if dbase == nil then 
		dbase, new_data = original, true
	else
		for name in pairs(dbase) do
			local found_sector = false

			for oname in pairs(original) do
				if name == oname then
					found_sector = true
				end
			end

			if not found_sector then
				dbase[name] = nil
			end
		end

		for name, val in pairs(original) do
			if dbase[name] == nil then	
				dbase[name], corrupted_data = val, true
				missing_sectors[#missing_sectors+1] = '*' .. name
			else
				local corrupted_sector = false
				for sname, sdata in pairs(val) do
					if sname ~= 'keybinds' and dbase[name][sname] == nil or type(sdata) ~= type(dbase[name][sname]) then
						dbase[name][sname], corrupted_data = sdata, true

						if not corrupted_sector then
							missing_sectors[#missing_sectors+1] = '*' .. name
							corrupted_sector = true
						end
					end
				end
			end
		end

		if #missing_sectors > 0 then
			client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
			client_color_log(255, 255, 255, ('Repairing %d sector(s) \1\0'):format(#missing_sectors))
			client_color_log(155, 220, 220, ('[ %s ]'):format(table_concat(missing_sectors, ' ')))
		end
	end

	if new_data or corrupted_data then
		database_write(db_name, dbase)
	end

	return dbase, original
end

local script_name = 'idealyaw'
local database_name = 'idealyaw'
local menu_tab = { 'LUA', 'A', 'B' }
local menu_palette = { 'Solid', 'Fade', 'Dynamic fade' }
local m_hotkeys, m_hotkeys_update, m_hotkeys_create = { }, true

local ms_watermark = ui_new_checkbox('CONFIG', 'Presets', 'Watermark')
local ms_spectators = ui_new_checkbox('CONFIG', 'Presets', 'Spectators')
local ms_keybinds = ui_new_checkbox('CONFIG', 'Presets', 'Hotkey list')
local ms_antiaim = ui_new_checkbox('CONFIG', 'Presets', 'Anti-aimbot indication')
local ms_ieinfo = ui_new_checkbox('CONFIG', 'Presets', 'Frequency update information')

local ms_palette, ms_color = 
	ui_new_combobox('CONFIG', 'Presets', 'idealyaw Palette', menu_palette),
	ui_new_color_picker('CONFIG', 'Presets', 'idealyaw Global color', 142, 165, 229, 85)

local ms_fade_offset = ui_new_slider('CONFIG', 'Presets', 'Fade offset', 1, 1000, 825, false, nil, 0.001)
local ms_fade_frequency = ui_new_slider('CONFIG', 'Presets', 'Fade frequency', 1, 100, 10, false, nil, 0.01)
local ms_fade_split_ratio = ui_new_slider('CONFIG', 'Presets', 'Fade split ratio', 0, 100, 100, false, nil, 0.01)

local script_db, original_db = read_database(script_name, database_name, {
	watermark = {
		nickname = '',		
		beta_status = true,
		gc_state = true,
		style = create_integer(1, 4, 1, 1),
		suffix = nil,
	},

	spectators = {
		avatars = true,
		auto_position = true
	},

	keybinds = {
		{
			require = '',
			reference = { 'legit', 'aimbot', 'Enabled' },
			custom_name = 'Legit aimbot',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'legit', 'triggerbot', 'Enabled' },
			custom_name = 'Legit triggerbot',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Enabled' },
			custom_name = 'Rage aimbot',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Force safe point' },
			custom_name = 'Force safe point',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Force body aim' },
			custom_name = 'Force body aim',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Override hitbox selection' },
			custom_name = 'Hitbox override',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Minimum damage override' },
			custom_name = 'Min damage override',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Hide shots' },
			custom_name = 'Hide shots',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'aimbot', 'Double tap' },
			custom_name = 'Double tap',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'other', 'Quick peek assist' },
			custom_name = 'Quick peek assist',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'other', 'Quick stop' },
			custom_name = 'Quick stop',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'rage', 'other', 'Duck peek assist' },
			custom_name = 'Duck peek assist',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'rage', 'other', 'Anti-aim correction override' },
			custom_name = 'Resolver override',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'aa', 'anti-aimbot angles', 'Inverter' },
			custom_name = 'Inverter',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'aa', 'anti-aimbot angles (2)', 'Freestanding' },
			custom_name = 'Freestanding',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'aa', 'other', 'Slow motion' },
			custom_name = 'Slow motion',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'aa', 'other', 'On shot anti-aim' },
			custom_name = 'On shot anti-aim',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'aa', 'other', 'Fake duck' },
			custom_name = 'Fake duck',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'aa', 'other', 'Fake peek' },
			custom_name = 'Fake peek',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'movement', 'Z-Hop' },
			custom_name = 'Z-Hop',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'movement', 'Pre-speed' },
			custom_name = 'Pre-speed',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'movement', 'Blockbot' },
			custom_name = 'Blockbot',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'movement', 'Jump at edge' },
			custom_name = 'Jump at edge',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'movement', 'Edge bug' },
			custom_name = 'Edge bug',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Last second defuse' },
			custom_name = 'Last second defuse',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Free look' },
			custom_name = 'Free look',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Ping spike' },
			custom_name = 'Ping spike',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Automatic grenade release' },
			custom_name = 'Grenade release',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Grenade prediction' },
			custom_name = 'Grenade prediction',
			ui_offset = 1
		},

		{
			require = '',
			reference = { 'misc', 'miscellaneous', 'Steal name' },
			custom_name = 'Steal name',
			ui_offset = 2
		},

		{
			require = '',
			reference = { 'visuals', 'player esp', 'Activation type' },
			custom_name = 'ESP Activation',
			ui_offset = 1
		},
	},
})

local get_bar_color = function()
	local r, g, b, a = ui_get(ms_color)

	local palette = ui_get(ms_palette)

	if palette ~= menu_palette[1] then
		local rgb_split_ratio = ui_get(ms_fade_split_ratio) / 100

		local h = palette == menu_palette[3] and 
			globals_realtime() * (ui_get(ms_fade_frequency) / 100) or 
			ui_get(ms_fade_offset) / 1000

		r, g, b = hsv_to_rgb(h, 1, 1, 1)
		r, g, b = 
			r * rgb_split_ratio, 
			g * rgb_split_ratio, 
			b * rgb_split_ratio
	end

	return r, g, b, a
end

local get_color = function(number, max, i)
    local Colors = {
        { 255, 0, 0 },
        { 237, 27, 3 },
        { 235, 63, 6 },
        { 229, 104, 8 },
        { 228, 126, 10 },
        { 220, 169, 16 },
        { 213, 201, 19 },
        { 176, 205, 10 },
        { 124, 195, 13 }
    }

    local math_num = function(int, max, declspec)
        local int = (int > max and max or int)
        local tmp = max / int;

        if not declspec then declspec = max end

        local i = (declspec / tmp)
        i = (i >= 0 and math_floor(i + 0.5) or math_ceil(i - 0.5))

        return i
    end

    i = math_num(number, max, #Colors)

    return
        Colors[i <= 1 and 1 or i][1], 
        Colors[i <= 1 and 1 or i][2],
        Colors[i <= 1 and 1 or i][3],
        i
end

local ms_classes = {
	watermark = function()
		local note = notes 'a_watermark'
		local cstyle = { [1] = 'gamesense ', [2] = 'idealyaw', [3] = 'brother-tech', [4] = 'skeet.cc' }
	
		local has_beta = pcall(ui_reference, 'misc', 'Settings', 'Crash logs')
		local get_name = panorama_loadstring([[ return MyPersonaAPI.GetName() ]])
		local get_gc_state = panorama_loadstring([[ return MyPersonaAPI.IsConnectedToGC() ]])
	
		local classptr = ffi.typeof('void***')
		local latency_ptr = ffi.typeof('float(__thiscall*)(void*, int)')
	
		local rawivengineclient = client_create_interface('engine.dll', 'VEngineClient014') or error('VEngineClient014 wasnt found', 2)
		local ivengineclient = ffi.cast(classptr, rawivengineclient) or error('rawivengineclient is nil', 2)
		local is_in_game = ffi.cast('bool(__thiscall*)(void*)', ivengineclient[0][26]) or error('is_in_game is nil')

	
		local g_paint_handler = function()
			local state = ui_get(ms_watermark)
			local r, g, b, a = get_bar_color()
	
			note.set_state(state)
	
			note.get(function(id)
				local data_wm = script_db.watermark or { }
				local data_nickname = data_wm.nickname and tostring(data_wm.nickname) or ''
				local data_suffix = (data_wm.suffix and tostring(data_wm.suffix) or ''):gsub('beta', '')
	
				if data_wm.beta_status and has_beta and (not data_suffix or #data_suffix < 1) then
					data_suffix = 'beta'
				end
	
				local sys_time = { client_system_time() }
				local actual_time = ('%02d:%02d:%02d'):format(sys_time[1], sys_time[2], sys_time[3])
	
				local is_connected_to_gc = not data_wm.gc_state or get_gc_state()
				local gc_state = not is_connected_to_gc and '\x20\x20\x20\x20\x20' or ''
	
				local nickname = #data_nickname > 0 and data_nickname or get_name()
				local suffix = ('%s%s'):format(
					cstyle[data_wm.style and data_wm.style.value or 1] or cstyle[1], 
					#data_suffix > 0 and (' [%s]'):format(data_suffix) or ''
				)
				
				local latency = math.floor(client.latency() * 1000)
				local latency_text = (' | delay: %3dms'):format(latency)

	
				local text = ('%s%s | %s%s | %s'):format(gc_state, suffix, nickname, latency_text, actual_time)
	
				local text_prefix = suffix:find("idealyaw") and "ideal" or suffix
				local text_colored = suffix:find("idealyaw") and "yaw" or ""
				local rest = (" | %s%s | %s"):format(nickname, latency_text, actual_time)

	
				local w = renderer_measure_text(nil, text_prefix)
					+ renderer_measure_text(nil, text_colored)
					+ renderer_measure_text(nil, rest)
					+ 4 + 22 
			        - 6
	
				local h = 18
				local x, y = client_screen_size(), 10 + (25*id)
				x = x - w - 10
	
				if ui_get(ms_palette) == menu_palette[1] then
					renderer_rectangle(x, y, w, 2, r, g, b, 255)
				else
					renderer_gradient(x, y, (w/2)+1, 2, g, b, r, 255, r, g, b, 255, true)
					renderer_gradient(x + w/2, y, w-w/2, 2, r, g, b, 255, b, r, g, 255, true)
				end
	
				renderer_rectangle(x, y + 2, w, h, 17, 17, 17, a)
	
				if icon and icon.texture then
					renderer_texture(icon.texture, x + 4, y + 4, 16, 16, 255, 255, 255, 255, 'f')
				end
	
				local offset = 24 
				renderer_text(x + offset -8, y + 4, 255, 255, 255, 255, '', 0, text_prefix)
				offset = offset + renderer_measure_text(nil, text_prefix)
	
				renderer_text(x + offset -8, y + 4, 173, 216, 230, 255, '', 0, text_colored)
				offset = offset + renderer_measure_text(nil, text_colored)
	
				renderer_text(x + offset -8, y + 4, 255, 255, 255, 255, '', 0, rest)
	
				if not is_connected_to_gc then
					local realtime = globals_realtime()*1.5
					
					if realtime%2 <= 1 then
						renderer_circle_outline(x+10, y + 11, 89, 119, 239, 255, 5, 0, realtime%1, 2)
					else
						renderer_circle_outline(x+10, y + 11, 89, 119, 239, 255, 5, realtime%1*370, 1-realtime%1, 2)
					end
				end
			end)
		end
	
		client_set_event_callback('paint_ui', g_paint_handler)
	end,

	spectators = function()
		local screen_size = { client_screen_size() }
		local screen_size = {
			screen_size[1] - screen_size[1] * cvar.safezonex:get_float(),
			screen_size[2] * cvar.safezoney:get_float()
		}

		local dragging = dragging_fn('Spectators', screen_size[1] / 1.385, screen_size[2] / 2)
		local m_alpha, m_active, m_contents, unsorted = 0, {}, {}, {}

		local get_spectating_players = function()
			local me = entity_get_local_player()

			local players, observing = { }, me
		
			for i = 1, globals_maxplayers() do
				if entity_get_classname(i) == 'CCSPlayer' then
					local m_iObserverMode = entity_get_prop(i, 'm_iObserverMode')
					local m_hObserverTarget = entity_get_prop(i, 'm_hObserverTarget')
		
					if m_hObserverTarget ~= nil and m_hObserverTarget <= 64 and not entity_is_alive(i) and (m_iObserverMode == 4 or m_iObserverMode == 5) then
						if players[m_hObserverTarget] == nil then
							players[m_hObserverTarget] = { }
						end
		
						if i == me then
							observing = m_hObserverTarget
						end
		
						table_insert(players[m_hObserverTarget], i)
					end
				end
			end
		
			return players, observing
		end

		local g_paint_handler = function()
			local data_sp = script_db.spectators or { }

			local master_switch = ui_get(ms_spectators)
			local is_menu_open = ui_is_menu_open()
			local frames = 8 * globals_frametime()
		
			local latest_item = false
			local maximum_offset = 85
		
			local me = entity_get_local_player()
			local spectators, player = get_spectating_players()
		
			for i=1, 64 do 
				unsorted[i] = {
					idx = i,
					active = false
				}
			end
		
			if spectators[player] ~= nil then
				for _, spectator in pairs(spectators[player]) do
					unsorted[spectator] = { 
						idx = spectator,
		
						active = (function()
							if spectator == me then
								return false
							end

							return true
						end)(),

						avatar = (function()
							if not data_sp.avatars then
								return nil
							end

							local steam_id = entity_get_steam64(spectator)
							local avatar = images.get_steam_avatar(steam_id)
		
							if steam_id == nil or avatar == nil then
								return nil
							end
		
							if m_contents[spectator] == nil or m_contents[spectator].conts ~= avatar.contents then
								m_contents[spectator] = {
									conts = avatar.contents,
									texture = renderer_load_rgba(avatar.contents, avatar.width, avatar.height)
								}
							end
		
							return m_contents[spectator].texture
						end)()
					}
				end
			end
		
			for _, c_ref in pairs(unsorted) do
				local c_id = c_ref.idx
				local c_nickname = entity_get_player_name(c_ref.idx)
		
				if c_ref.active then
					latest_item = true
		
					if m_active[c_id] == nil then
						m_active[c_id] = {
							alpha = 0, offset = 0, active = true
						}
					end
		
					local text_width = renderer_measure_text(nil, c_nickname)
		
					m_active[c_id].active = true
					m_active[c_id].offset = text_width
					m_active[c_id].alpha = m_active[c_id].alpha + frames
					m_active[c_id].avatar = c_ref.avatar
					m_active[c_id].name = c_nickname
		
					if m_active[c_id].alpha > 1 then
						m_active[c_id].alpha = 1
					end
				elseif m_active[c_id] ~= nil then
					m_active[c_id].active = false
					m_active[c_id].alpha = m_active[c_id].alpha - frames
		
					if m_active[c_id].alpha <= 0 then
						m_active[c_id] = nil
					end
				end
		
				if m_active[c_id] ~= nil and m_active[c_id].offset > maximum_offset then
					maximum_offset = m_active[c_id].offset
				end
			end
		
			if is_menu_open and not latest_item then
				local case_name = ' '
				local text_width = renderer_measure_text(nil, case_name)
		
				latest_item = true
				maximum_offset = maximum_offset < text_width and text_width or maximum_offset
		
				m_active[case_name] = {
					name = '',
					active = true,
					offset = text_width,
					alpha = 1
				}
			end
		
			local text = 'spectators'
			local x, y = dragging:get()
			local r, g, b, a = get_bar_color()
		
			local height_offset = 23
			local w, h = 55 + maximum_offset, 50
		
			w = w - (data_sp.avatars and 0 or 17) 

			local right_offset = data_sp.auto_position and (x+w/2) > (({ client_screen_size() })[1] / 2)

			if ui_get(ms_palette) == menu_palette[1] then
				renderer_rectangle(x, y, w, 2, r, g, b, m_alpha*255)
			else
				renderer_gradient(x, y, (w/2)+1, 2, g, b, r, m_alpha*255, r, g, b, m_alpha*255, true)
				renderer_gradient(x + w/2, y, w-w/2, 2, r, g, b, m_alpha*255, b, r, g, m_alpha*255, true)
			end

			renderer_rectangle(x, y + 2, w, 18, 17, 17, 17, m_alpha*a)
		
			renderer_text(x - renderer_measure_text(nil, text) / 2 + w/2, y + 4, 255, 255, 255, m_alpha*255, '', 0, text)
		
			for c_name, c_ref in pairs(m_active) do
				local _, text_h = renderer_measure_text(nil, c_ref.name)

				renderer_text(x + ((c_ref.avatar and not right_offset) and text_h or -5) + 10, y + height_offset, 255, 255, 255, m_alpha*c_ref.alpha*255, '', 0, c_ref.name)
		
				if c_ref.avatar ~= nil then
					renderer_texture(c_ref.avatar, x + (right_offset and w - 15 or 5), y + height_offset, text_h, text_h, 255, 255, 255, m_alpha*c_ref.alpha*255, 'f')
				end
		
				height_offset = height_offset + 15
			end

			dragging:drag(w, (3 + (15 * item_count(m_active))) * 2)

			if master_switch and item_count(m_active) > 0 and latest_item then
				m_alpha = m_alpha + frames; if m_alpha > 1 then m_alpha = 1 end
			else
				m_alpha = m_alpha - frames; if m_alpha < 0 then m_alpha = 0 end 
			end
		
			if is_menu_open then
				m_active[' '] = nil
			end
		end

		client_set_event_callback('paint', g_paint_handler)
	end,

	keybinds = function()
		local screen_size = { client_screen_size() }
		local screen_size = {
			screen_size[1] - screen_size[1] * cvar.safezonex:get_float(),
			screen_size[2] * cvar.safezoney:get_float()
		}

		local dragging = dragging_fn('Keybinds', screen_size[1] / 1.385, screen_size[2] / 2.5)

		local m_alpha, m_active = 0, { }
		local hotkey_modes = { 'holding', 'toggled', 'disabled' }

		local elements = {
			rage = { 'aimbot', 'other' },
			aa = { 'anti-aimbot angles', 'fake lag', 'other' },
			legit = { 'weapon type', 'aimbot', 'triggerbot', 'other' },
			visuals = { 'player esp', 'colored models', 'other esp', 'effects' },
			misc = { 'miscellaneous', 'movement', 'settings' },
			skins = { 'knife options', 'glove options', 'weapon skin' },
			players = { 'players', 'adjustments' },
			config = { 'presets', 'lua' },
			lua = { 'a', 'b' }
		}

		local reference_if_exists = function(...)
			if pcall(ui_reference, ...) then
				 return true
			end
		end

		local create_item = function(data)
			local collected = { }

			local cname = data.custom_name
			local reference = { ui_reference(unpack(data.reference)) }
		
			for i=1, #reference do
				if i <= data.ui_offset then
					collected[i] = reference[i]
				end
			end
		
			cname = (cname and #tostring(cname) > 0) and cname or nil

			data.reference[3] = data.ui_offset == 2 and ui_name(collected[1]) or data.reference[3]

			m_hotkeys[cname or (data.reference[3] or '?')] = {
				reference = data.reference,

				ui_offset = data.ui_offset,
				custom_name = cname,
				custom_file = data.require,
				collected = collected
			}

			return true
		end
		
		local create_custom_item = function(pdata)
			local reference = pdata.reference

			if  reference == nil or elements[reference[1]:lower()] == nil or 
				not contains(elements[reference[1]:lower()], reference[2]:lower()) then
				return false
			end

			if reference_if_exists(unpack(reference)) then
				return create_item(pdata)
			else
				if pcall(require, pdata.require) and reference_if_exists(unpack(reference)) then
					return create_item(pdata)
				else
					local name = (pdata.require and #pdata.require > 0) and (pdata.require .. '.lua') or '-'

					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(155, 220, 220, ('Unable to reference hotkey: %s [ %s ]'):format(reference[3], name))
				end
			end

			return false
		end

		local g_paint_handler = function()
			local master_switch = ui_get(ms_keybinds)

			local is_menu_open = ui_is_menu_open()
			local frames = 8 * globals_frametime()
		
			local latest_item = false
			local maximum_offset = 66

			if m_hotkeys_update == true then
				m_hotkeys = { }
				m_active = { }

				for _, item in pairs((script_db.keybinds or { })) do
					create_custom_item({
						reference = item.reference,
						custom_name = item.custom_name,
						ui_offset = item.ui_offset or 1,
						require = item.require
					})
				end

				m_hotkeys_update = false
			end
		
			for c_name, c_data in pairs(m_hotkeys) do
				local item_active = true
				local c_ref = c_data.collected

				local items = item_count(c_ref)
				local state = { ui_get(c_ref[items]) }
		
				if items > 1 then
					item_active = ui_get(c_ref[1])
				end
		
				if item_active and state[2] ~= 0 and (state[2] == 3 and not state[1] or state[2] ~= 3 and state[1]) then
					latest_item = true
		
					if m_active[c_name] == nil then
						m_active[c_name] = {
							mode = '', alpha = 0, offset = 0, active = true
						}
					end
		
					local text_width = renderer_measure_text(nil, c_name)
		
					m_active[c_name].active = true
					m_active[c_name].offset = text_width
					m_active[c_name].mode = hotkey_modes[state[2]]
					m_active[c_name].alpha = m_active[c_name].alpha + frames
		
					if m_active[c_name].alpha > 1 then
						m_active[c_name].alpha = 1
					end
				elseif m_active[c_name] ~= nil then
					m_active[c_name].active = false
					m_active[c_name].alpha = m_active[c_name].alpha - frames
		
					if m_active[c_name].alpha <= 0 then
						m_active[c_name] = nil
					end
				end
		
				if m_active[c_name] ~= nil and m_active[c_name].offset > maximum_offset then
					maximum_offset = m_active[c_name].offset
				end
			end
		
			if is_menu_open and not latest_item then
				local case_name = 'Menu toggled'
				local text_width = renderer_measure_text(nil, case_name)
		
				latest_item = true
				maximum_offset = maximum_offset < text_width and text_width or maximum_offset
		
				m_active[case_name] = {
					active = true,
					offset = text_width,
					mode = '~',
					alpha = 1,
				}
			end
		
			local text = 'keybinds'
			local x, y = dragging:get()
			local r, g, b, a = get_bar_color()
		
			local height_offset = 23
			local w, h = 75 + maximum_offset, 50
		
			if ui_get(ms_palette) == menu_palette[1] then
				renderer_rectangle(x, y, w, 2, r, g, b, m_alpha*255)
			else
				renderer_gradient(x, y, (w/2)+1, 2, g, b, r, m_alpha*255, r, g, b, m_alpha*255, true)
				renderer_gradient(x + w/2, y, w-w/2, 2, r, g, b, m_alpha*255, b, r, g, m_alpha*255, true)
			end

			renderer_rectangle(x, y + 2, w, 18, 17, 17, 17, m_alpha*a)
			renderer_text(x - renderer_measure_text(nil, text) / 2 + w/2, y + 4, 255, 255, 255, m_alpha*255, '', 0, text)
		
			for c_name, c_ref in pairs(m_active) do
				local key_type = '[' .. (c_ref.mode or '?') .. ']'
		
				renderer_text(x + 5, y + height_offset, 255, 255, 255, m_alpha*c_ref.alpha*255, '', 0, c_name)
				renderer_text(x + w - renderer_measure_text(nil, key_type) - 5, y + height_offset, 255, 255, 255, m_alpha*c_ref.alpha*255, '', 0, key_type)
		
				height_offset = height_offset + 15
			end
		
			dragging:drag(w, (3 + (15 * item_count(m_active))) * 2)

			if master_switch and item_count(m_active) > 0 and latest_item then
				m_alpha = m_alpha + frames

				if m_alpha > 1 then 
					m_alpha = 1
				end
			else
				m_alpha = m_alpha - frames

				if m_alpha < 0 then
					m_alpha = 0
				end 
			end
		
			if is_menu_open then
				m_active['Menu toggled'] = nil
			end
		end
		
		m_hotkeys_create = create_custom_item

		client_set_event_callback('paint', g_paint_handler)
	end,

	antiaim = function()
        local note = notes 'a_wbantiaim'
        
        local gram_fyaw = gram_create(0, 2)
        local teleport_data = gram_create(0, 3)

        local ind_phase, ind_num, ind_time = 0, 0, 0
        local last_sent, current_choke = 0, 0
        local teleport, last_origin = 0
        local breaking_lc = 0

        local g_setup_command = function(c)
            local me = entity_get_local_player()
        
            if c.chokedcommands == 0 then
                local m_origin = vector(entity_get_origin(me))
        
                if last_origin ~= nil then
                    teleport = (m_origin-last_origin):length2dsqr()
        
                    gram_update(teleport_data, teleport, true)
                end
        
                gram_update(gram_fyaw, math_abs(anti_aim.get_desync(1)), true)
        
                last_sent = current_choke
                last_origin = m_origin
            end
        
            breaking_lc = 
                get_average(teleport_data) > 3200 and 1 or
                    (anti_aim.get_tickbase_shifting() > 0 and 2 or 0)
        
            current_choke = c.chokedcommands
        end

        local g_paint_handler = function()
            note.set_state(false)
        
            local me = entity_get_local_player()
            
            if me == nil or not entity_is_alive(me) then
                return
            end
        
            local state = ui_get(ms_antiaim)
            local _, _, _, a = get_bar_color()
        
            note.set_state(state)
            note.get(function(id)
                local ms_clr = { ui_get(ms_color) }
        
                local addr, nval = '', false
                local r, g, b = 150, 150, 150
        
                local fr = globals_frametime() * 3.75
                local min_offset = 1200+math_max(0, get_average(teleport_data)-3800)
                local teleport_mt = math_abs(math_min(teleport-3800, min_offset) / min_offset * 100)
        
                if ind_num ~= teleport_mt and ind_time < globals_realtime() then
                    ind_time = globals_realtime() + 0.005
                    ind_num = ind_num + (ind_num > teleport_mt and -1 or 1)
                end
        
                ind_phase = ind_phase + (breaking_lc == 1 and fr or -fr)
                ind_phase = ind_phase > 1 and 1 or ind_phase
                ind_phase = ind_phase < 0 and 0 or ind_phase
        
                if breaking_lc == 2 then
                    addr, ind_phase, ind_num = ' | SHIFTING', 0, 0
                    r, g, b = 228, 126, 10
                elseif ind_phase > 0.1 then
                    addr = ' | dst: \x20\x20\x20\x20\x20\x20\x20\x20\x20'
                end
        
                local text = ('FL: %s%s'):format(
                    (function()
                        if tonumber(last_sent) < 10 then
                            return '\x20\x20' .. last_sent
                        end

                        return last_sent
                    end)(),
                addr)
                
                local h, w = 17, renderer_measure_text(nil, text) + 8
                local x, y = client_screen_size(), 10 + (25*id)
        
                x = x - w - 10
        
                renderer_gradient(x, y + h, w/2, 1, 0, 0, 0, 25, r, g, b, 255, true)
                renderer_gradient(x + w/2, y + h, w - w/2, 1, r, g, b, 255, 0, 0, 0, 25, true)
        
                renderer_rectangle(x, y, w, h, 17, 17, 17, a)
                renderer_text(x+4, y + 2, 255, 255, 255, 255, '', 0, text)
        
                if ind_phase > 0 then
                    renderer_gradient(
                        x + w - renderer_measure_text(nil, ' | dst: ') + 2, 
                        y + 6, math_min(100, ind_num) / 100 * 24, 5,
        
                        ms_clr[1], ms_clr[2], ms_clr[3], ind_phase*220,
                        ms_clr[1], ms_clr[2], ms_clr[3], ind_phase * 25,
        
                        true
                    )
                end
        
                -- FAKE INDICATION
                local lower_body = anti_aim.get_balance_adjust()
                local r, g, b = get_color(math_abs(anti_aim.get_desync()), 30)
        
                local timer = (lower_body.next_update - globals_curtime()) / 1.1 * 1
                local add_text = (lower_body.updating and timer >= 0) and '\x20\x20\x20\x20\x20' or ''
        
                local text = ('%sFAKE (%.1f°)'):format(add_text, get_average(gram_fyaw))
                local h, w = 18, renderer_measure_text(nil, text) + 8
        
                -- INDICATIN GRADIENT
                local dec = { r - (r/100 * 50), g - (g/100 * 50), b - (b/100 * 50) }
        
                renderer_gradient(x - w - 6, y, 2, h / 2, dec[1], dec[2], dec[3], 0, r, g, b, 255, false)
                renderer_gradient(x - w - 6, y + h/2, 2, h / 2, r, g, b, 255, dec[1], dec[2], dec[3], 0, false)
        
                -- BACKGROUND GRADIENT
                renderer_gradient(x - w - 4, y, w / 2, h, 17, 17, 17, 25,  17, 17, 17, a, true)
                renderer_gradient(x - w - 4 + w / 2, y, w / 2, h, 17, 17, 17, a,  17, 17, 17, 25, true)
                renderer_text(x - w, y + 2, 255, 255, 255, 255, '', 0, text)
        
                if lower_body.updating and timer >= 0 then
                    renderer_circle_outline(x - w + 6, y + 8.5, 89, 119, 239, 255, 5, 0, timer, 2)
                end
            end)
        end

        client_set_event_callback('setup_command', g_setup_command)
        client_set_event_callback('paint_ui', g_paint_handler)
	end,

    ilstate = function()
		local note = notes 'a_winput'
        local graphics = graphs()
		
        local formatting = (function(avg)
            if avg < 1 then return ('%.2f'):format(avg) end
            if avg < 10 then return ('%.1f'):format(avg) end
            return ('%d'):format(avg)
        end)

        local jmp_ecx = client_find_signature('engine.dll', '\xFF\xE1')
        local fnGetModuleHandle = ffi.cast('uint32_t(__fastcall*)(unsigned int, unsigned int, const char*)', jmp_ecx)
        local fnGetProcAddress = ffi.cast('uint32_t(__fastcall*)(unsigned int, unsigned int, uint32_t, const char*)', jmp_ecx)
        
        local pGetProcAddress = ffi.cast('uint32_t**', ffi.cast('uint32_t', client_find_signature('engine.dll', '\xFF\x15\xCC\xCC\xCC\xCC\xA3\xCC\xCC\xCC\xCC\xEB\x05')) + 2)[0][0]
        local pGetModuleHandle = ffi.cast('uint32_t**', ffi.cast('uint32_t', client_find_signature('engine.dll', '\xFF\x15\xCC\xCC\xCC\xCC\x85\xC0\x74\x0B')) + 2)[0][0]
        local BindExports = function(sModuleName, sFunctionName, sTypeOf) local ctype = ffi.typeof(sTypeOf) return function(...) return ffi.cast(ctype, jmp_ecx)(fnGetProcAddress(pGetProcAddress, 0, fnGetModuleHandle(pGetModuleHandle, 0, sModuleName), sFunctionName), 0, ...) end end
        
        local fnEnumDisplaySettingsA = BindExports("user32.dll", "EnumDisplaySettingsA", "int(__fastcall*)(unsigned int, unsigned int, unsigned int, unsigned long, void*)");
        local pLpDevMode = ffi.new("struct { char pad_0[120]; unsigned long dmDisplayFrequency; char pad_2[32]; }[1]")
        
        local gram_create = function(value, count) local gram = { }; for i=1, count do gram[i] = value; end return gram; end
        local gram_update = function(tab, value, forced) local new_tab = tab; if forced or new_tab[#new_tab] ~= value then table_insert(new_tab, value); table_remove(new_tab, 1); end; tab = new_tab; end
        local get_average = function(tab) local elements, sum = 0, 0; for k, v in pairs(tab) do sum = sum + v; elements = elements + 1; end return sum / elements; end
        
        local renderTime = client_timestamp()
        local lag_data = gram_create(0, 90)
        local fps_data = gram_create(0, 30)
        local g_frameRate, g_prev_frameRate = 0, 0
        
        local post_render, pre_render = function()
            renderTime = client_timestamp()
        end, function()
            gram_update(lag_data, client_timestamp() - renderTime)
        end
        
        client_set_event_callback('post_render', post_render)
        client_set_event_callback('pre_render', pre_render)

        fnEnumDisplaySettingsA(0, 4294967295, pLpDevMode[0])

		local g_paint_handler = function()
            g_frameRate = 0.9 * g_frameRate + (1.0 - 0.9) * globals_absoluteframetime()
            gram_update(fps_data, math_abs(g_prev_frameRate-(1/g_frameRate)), true)
            g_prev_frameRate = 1/g_frameRate

			local state = ui_get(ms_ieinfo)
			local _, _, _, a = get_bar_color()

            note.set_state(state)
			note.get(function(id)
                local avg = get_average(lag_data)
                local display_frequency = tonumber(pLpDevMode[0].dmDisplayFrequency)
				local text = ('%sms / 144hz'):format(formatting(avg), display_frequency)
		
                local interp = { get_color(15-avg, 15) }

				local h, w = 18, renderer_measure_text(nil, text) + 8
				local x, y = client_screen_size(), 10 + (25*id)
		
				x = x - w - 10

                renderer_gradient(x, y+h, (w/2), 1, 0, 0, 0, 25, interp[1], interp[2], interp[3], 255, true)
                renderer_gradient(x + w/2, y+h, w-w/2, 1, interp[1], interp[2], interp[3], 255, 0, 0, 0, 25, true)

				renderer_rectangle(x, y, w, h, 17, 17, 17, a)
				renderer_text(x+4, y + 2, 255, 255, 255, 255, '', 0, text)

                local text = 'IO | '
                local sub = text .. '\x20\x20\x20\x20\x20\x20\x20'
                local h, w = 18, renderer_measure_text(nil, sub) + 8
                local ie_w = renderer_measure_text(nil, text) + 4
                local r, g, b = ui_get(ms_color)

                local g_nValues_t = { 
                    avg, 1, 3, 
                    get_average(fps_data)/4, 0
                }

                local min_value, max_value = 
                    math_min(unpack(g_nValues_t)), 
                    math_max(unpack(g_nValues_t))

                renderer_rectangle(x - w - 4, y, w, h, 17, 17, 17, a)
                renderer_text(x - w, y + 2, 255, 255, 255, 255, '', 0, sub)

                graphics:draw_histogram(g_nValues_t, 0, max_value, #g_nValues_t, {
                    -- x, y, w, h
                    x = x - w - 4 + ie_w,
                    y = y + 4, 
                    w = w - ie_w - 4,
                    h = h - 8,
            
                    sDrawBar = "gradient_fadein", -- "none", "fill", "gradient_fadeout", "gradient_fadein"
                    bDrawPeeks = false,
                    thickness = 1,
            
                    clr_1 = { r, g, b, 255 },
                    clr_2 = { 0, 127, 255, 255 },
                }, false)
			end)
		end

		client_set_event_callback('paint_ui', g_paint_handler)
    end,

	editor = function()
		local data_editor = function()
			local editor, editor_data, editor_cache, editor_callback = 
				ui_new_checkbox(menu_tab[1], menu_tab[2], 'Idealyaw Data editor'), { }, { }, function() end
			
			for name, val in pairs(script_db) do
				if name ~= 'keybinds' then
					table_insert(editor_data, ui_new_label(menu_tab[1], menu_tab[2], name:upper()))
	
					for sname, sval in pairs(val) do
						local sval_type = type(sval)

						local _action = {
							['string'] = function()
								local _cfunction
								local label, textbox = 
									ui_new_label(menu_tab[1], menu_tab[2], ('	  > %s \n %s:%s'):format(sname, name, sname)), 
									ui_new_textbox(menu_tab[1], menu_tab[2], ('%s:%s'):format(name, sname))
	
								ui_set(textbox, script_db[name][sname])
	
								_cfunction = function()
									script_db[name][sname] = ui_get(textbox)
									client_delay_call(0.01, function()
										_cfunction()
									end)
								end
	
								_cfunction()
	
								return { label, textbox }
							end,
	
							['boolean'] = function()
								local checkbox = ui_new_checkbox(menu_tab[1], menu_tab[2], ('	  > %s \n %s:%s'):format(sname, name, sname))
	
								ui_set(checkbox, sval)
								ui_set_callback(checkbox, function(c)
									script_db[name][sname] = ui_get(c)
								end)
	
								return { checkbox }
							end,
	
							['table'] = function()
								local slider = ui_new_slider(menu_tab[1], menu_tab[2], ('	  > %s \n %s:%s'):format(sname, name, sname), sval.min, sval.max, sval.init_val, true, nil, sval.scale)
	
								ui_set(slider, sval.value or sval.init_val)
								ui_set_callback(slider, function(c)
									script_db[name][sname].value = ui_get(c)
								end)
	
								return { slider }
							end
						}
	
						if _action[sval_type] ~= nil then
							for _, val in pairs(_action[sval_type]()) do
								table_insert(editor_data, val)
							end
						end
					end
				end
			end
	
			local pre_config_save = function()
				ui_set(editor, false)
	
		
				for _, ref in pairs(editor_data) do
					editor_cache[ref] = ui_get(ref)
				end
			end
		
			local post_config_save = function()
				ui_set(editor, false)
				
				for _, ref in pairs(editor_data) do
					if editor_cache[ref] ~= nil then
						ui_set(ref, editor_cache[ref])
						editor_cache[ref] = nil
					end
				end
			end
		
			client_set_event_callback('pre_config_save', function() pre_config_save() end)
			client_set_event_callback('post_config_save', function() post_config_save() end)
			client_set_event_callback('pre_config_load', function() pre_config_save() end)
			client_set_event_callback('post_config_load', function() post_config_save() end)
	
			editor_callback = function()
				local editor_active = ui_get(editor)
		
				for _, ref in pairs(editor_data) do
					ui_set_visible(ref, editor_active)
				end
			end
		
			ui_set_callback(editor, editor_callback)
			editor_callback()
		end
	
		local keybind_editor = function()
			local create_table = function(tbl)
				local new_table = { }
		
				for k in pairs(tbl) do
					table_insert(new_table, k)
				end
			
				table_sort(new_table, function(a, b) 
					return a:lower() < b:lower() 
				end)
		
				local new_table2 = { 
					'» Create new keybind'
				}
		
				for i=1, #new_table do
					table_insert(new_table2, new_table[i])
				end
		
				return new_table2
			end
		
			local generate_kb = function()
				local new_table = { }
				
				for id, hotkey in pairs(script_db.keybinds) do
					local custom_name = hotkey.custom_name
					custom_name = (custom_name and #tostring(custom_name) > 0) and custom_name or nil
	
					new_table[custom_name or (hotkey.reference[3] or '?')] = {
						hotkey_id = id,
						reference = hotkey.reference,
						custom_name = hotkey.custom_name,
						ui_offset = hotkey.ui_offset,
						require = hotkey.require
					}
				end
	
				return new_table
			end
			
			local hk_callback, listbox_callback
			local original_hk = {
				reference = { '', '', '' },
				custom_name = '',
				ui_offset = 1,
				require = ''
			}
	
			local offset_type = {
				'Basic',
				'Extended'
			}
	
			local new_hotkey = original_hk
			
			local hk_database = generate_kb()
			local hk_list = create_table(hk_database)
	
			local hk_editor = ui_new_checkbox(menu_tab[1], menu_tab[2], 'Idealyaw Hotkey editor')
			local listbox = ui_new_listbox(menu_tab[1], menu_tab[2], 'Idealyaw Keybinds', hk_list)
		
			local require = {
				ui_new_checkbox(menu_tab[1], menu_tab[2], 'Custom hotkey'),
		
				ui_new_label(menu_tab[1], menu_tab[2], 'File name (without ".lua")'),
				ui_new_textbox(menu_tab[1], menu_tab[2], 'idealyaw:keybinds:required_file')
			}
		
			local custom_name = {
				ui_new_checkbox(menu_tab[1], menu_tab[2], 'Custom name'),
				ui_new_label(menu_tab[1], menu_tab[2], 'Original name'),
				ui_new_textbox(menu_tab[1], menu_tab[2], 'idealyaw:keybinds:custom_name')
			}
	
			local reference = {
				ui_new_label(menu_tab[1], menu_tab[2], 'Reference'),
				ui_new_textbox(menu_tab[1], menu_tab[2], 'idealyaw:keybinds:reference1'),
				ui_new_textbox(menu_tab[1], menu_tab[2], 'idealyaw:keybinds:reference2'),
				ui_new_textbox(menu_tab[1], menu_tab[2], 'idealyaw:keybinds:reference3')
			}
	
			local ui_offset = {
				ui_new_combobox(menu_tab[1], menu_tab[2], 'Hotkey type', offset_type),
				ui_new_hotkey(menu_tab[1], menu_tab[3], ('Example: %s'):format(offset_type[1])),
	
				ui_new_checkbox(menu_tab[1], menu_tab[3], ('Example: %s'):format(offset_type[2])),
				ui_new_hotkey(menu_tab[1], menu_tab[3], ' ', true),
	
				ui_new_combobox(menu_tab[1], menu_tab[3], ('Example: %s'):format(offset_type[2]), '-'),
				ui_new_hotkey(menu_tab[1], menu_tab[3], ' ', true),
			}
	
			local save_changes = ui_new_button(menu_tab[1], menu_tab[2], 'Save Changes', function()
				local selected = hk_list[ui_get(listbox)+1] or hk_list[1]
				local ui_offset = ui_get(ui_offset[1]) == offset_type[2] and 2 or 1
	
				local reference = { ui_get(reference[2]):lower(), ui_get(reference[3]):lower(), ui_get(reference[4]) }
				local custom_name = ui_get(custom_name[1]) and ui_get(custom_name[3]) or ''
	
				if selected ~= hk_list[1] then
					local cdata = hk_database[selected]
	
					if cdata ~= nil then
						script_db.keybinds[cdata.hotkey_id] = {
							ui_offset = ui_offset,
							reference = reference,
							require = ui_get(require[1]) and ui_get(require[3]):lower() or '',
							custom_name = custom_name
						}
					end
				else
					local can_create, item = true, {
						ui_offset = ui_offset,
						reference = reference,
						require = ui_get(require[1]) and ui_get(require[3]) or '',
						custom_name = custom_name
					}
	
					local item_ref = { 
						item.reference[1]:lower(),
						item.reference[2]:lower(),
						item.reference[3]:lower()
					}
	
					for id, val in pairs(script_db.keybinds) do
						local val_ref = { 
							val.reference[1]:lower(),
							val.reference[2]:lower(),
							val.reference[3]:lower()
						}
	
						if val_ref[1] == item_ref[1] and val_ref[2] == item_ref[2] and val_ref[3] == item_ref[3] then
							can_create = false
							break
						end
					end
	
					if can_create and m_hotkeys_create(item) then
						script_db.keybinds[#script_db.keybinds+1] = item
	
						client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
						client_color_log(255, 255, 255, 'Created hotkey \1\0')
						client_color_log(155, 220, 220, ('[ %s ]'):format(table_concat(item.reference, ' > ')))
					end
	
					if not can_create then
						client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
						client_color_log(255, 255, 255, 'Could\'nt create hotkey \1\0')
						client_color_log(155, 220, 220, '[ keybind already exists ]')
						error()
					end
				end
	
				m_hotkeys_update = true
	
				hk_database = generate_kb()
				hk_list = create_table(hk_database)
	
				ui_update(listbox, hk_list)
				
				listbox_callback(listbox)
				hk_callback()
			end)
	
			local delete_hk = ui_new_button(menu_tab[1], menu_tab[2], 'Delete Hotkey', function()
				local selected = hk_list[ui_get(listbox)+1] or hk_list[1]
	
				if selected ~= hk_list[1] then
					local cdata = hk_database[selected]
	
					script_db.keybinds[cdata.hotkey_id] = nil
	
					local new_db = { }
	
					for i=1, #script_db.keybinds do
						if script_db.keybinds[i] ~= nil then
							new_db[#new_db+1] = script_db.keybinds[i]
						end
					end
	
					script_db.keybinds = new_db
	
					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(255, 255, 255, 'Removed hotkey \1\0')
					client_color_log(155, 220, 220, ('[ %s ]'):format(table_concat(cdata.reference, ' > ')))
	
					m_hotkeys_update = true
	
					hk_database = generate_kb()
					hk_list = create_table(hk_database)
		
					ui_update(listbox, hk_list)
					
					listbox_callback(listbox)
					hk_callback()
					
				end
			end)
		
			hk_callback = function()
				local active = ui_get(hk_editor)
				local LBC = ui_get(listbox) == 0
		
				ui_set_visible(listbox, active)
		
				ui_set_visible(require[1], active and LBC)
				ui_set_visible(require[2], active and ui_get(require[1]) and LBC)
				ui_set_visible(require[3], active and ui_get(require[1]) and LBC)
		
				ui_set_visible(custom_name[1], active)
				ui_set_visible(custom_name[2], active and ui_get(custom_name[1]) and not LBC)
				ui_set_visible(custom_name[3], active and ui_get(custom_name[1]))
	
				ui_set_visible(reference[1], active)
				ui_set_visible(reference[2], active and LBC)
				ui_set_visible(reference[3], active and LBC)
				ui_set_visible(reference[4], active and LBC)
	
				ui_set_visible(save_changes, active)
				ui_set_visible(delete_hk, active and not LBC)
	
				for i=1, #ui_offset do
					ui_set_visible(ui_offset[i], active and LBC)
				end
			end
	
			listbox_callback = function(c)
				local local_bd = hk_database
				local selected = hk_list[ui_get(c)+1] or hk_list[1]
	
				local cdata = local_bd[selected]
	
				if cdata == nil then
					cdata = new_hotkey
				end
	
				local ext_data = {
					require = { #cdata.require > 0, cdata.require or '' },
					custom_name = { cdata.custom_name ~= '', ('Original name: %s'):format(cdata.reference[3]), cdata.custom_name },
	
					reference = { 
						('Reference: %s > %s (%d)'):format(cdata.reference[1], cdata.reference[2], cdata.ui_offset), 
						cdata.reference[1], cdata.reference[2], cdata.reference[3]
					},
	
					ui_offset = cdata.ui_offset
				}
	
				ui_set(reference[1], selected ~= hk_list[1] and ext_data.reference[1] or 'Reference')
	
				ui_set(require[1], ext_data.require[1])
				ui_set(require[3], ext_data.require[2])
			
				ui_set(custom_name[1], ext_data.custom_name[1])
				ui_set(custom_name[2], ext_data.custom_name[2])
				ui_set(custom_name[3], ext_data.custom_name[3])
	
				ui_set(reference[2], ext_data.reference[2])
				ui_set(reference[3], ext_data.reference[3])
				ui_set(reference[4], ext_data.reference[4])
	
				ui_set(ui_offset[1], offset_type[ext_data.ui_offset])
	
				hk_callback()
			end
	
			client_set_event_callback('pre_config_save', function() ui_set(hk_editor, false) end)
			client_set_event_callback('post_config_load', function() ui_set(hk_editor, false) end)
	
			ui_set_callback(hk_editor, hk_callback)
			ui_set_callback(listbox, listbox_callback)
			ui_set_callback(require[1], hk_callback)
			ui_set_callback(custom_name[1], hk_callback)
		
			hk_callback()
	
			return hk_editor
		end
	
		client_set_event_callback('console_input', function(e)
			local e = e:gsub(' ', '')
			local _action = {
				['idealyaw:watermark:set_suffix'] = function()
					script_db.watermark.suffix = ''
					database_write(database_name, script_db)
		
					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(155, 220, 220, 'Suffix is now active')
	
					client_reload_active_scripts()
				end,
	
				['idealyaw:watermark:unset_suffix'] = function()
					script_db.watermark.suffix = nil
					database_write(database_name, script_db)
		
					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(155, 220, 220, 'Suffix is now inactive')
	
					client_reload_active_scripts()
				end,
	
				['idealyaw:reset'] = function()
					for name in pairs(script_db) do
						script_db[name] = name == 'keybinds' and script_db.keybinds or { }
					end
	
					database_write(database_name, script_db)
	
					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(255, 0, 0, 'Wiping data sectors')
	
					client_reload_active_scripts()
				end,
	
				['idealyaw:keybinds:reset'] = function()
					script_db.keybinds = original_db.keybinds
	
					database_write(database_name, script_db)
	
					client_color_log(216, 181, 121, ('[%s] \1\0'):format(script_name))
					client_color_log(255, 0, 0, 'Wiping keybinds sector')
	
					client_reload_active_scripts()
				end
			}
	
			if _action[e] ~= nil then
				_action[e]()
	
				return true
			end
		end)
	
		data_editor()
		keybind_editor()
	end
}

ms_classes.watermark()
ms_classes.spectators()
ms_classes.keybinds()
ms_classes.antiaim()
ms_classes.ilstate()

client_delay_call(0.1, ms_classes.editor)
client_set_event_callback('shutdown', function()
	database_write(database_name, script_db)
end)

local ms_fade_callback = function()
	local active = ui_get(ms_palette)

	ui_set_visible(ms_fade_offset, active ~= menu_palette[1] and active == menu_palette[2])
	ui_set_visible(ms_fade_frequency, active ~= menu_palette[1] and active == menu_palette[3])
	ui_set_visible(ms_fade_split_ratio, active ~= menu_palette[1])
end

ui_set_callback(ms_palette, ms_fade_callback)
ms_fade_callback()

--==[ idealyaw_velocity.lua ]==--
local images = require "gamesense/images"

local warning = images.load_svg([[
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="360px" height="321px" style="shape-rendering:geometricPrecision; text-rendering:geometricPrecision; image-rendering:optimizeQuality; fill-rule:evenodd; clip-rule:evenodd" xmlns:xlink="http://www.w3.org/1999/xlink">
<g><path style="opacity:0.542" fill="#06040b" d="M 172.5,3.5 C 190.953,2.3096 205.453,9.3096 216,24.5C 257.667,96.5 299.333,168.5 341,240.5C 348.222,251.825 351.555,264.159 351,277.5C 347.84,294.329 338.007,305.163 321.5,310C 316.877,310.958 312.21,311.625 307.5,312C 222.167,312.667 136.833,312.667 51.5,312C 17.9834,308.505 4.48344,290.338 11,257.5C 12.2215,253.29 13.8882,249.29 16,245.5C 57.586,173.997 98.9193,102.33 140,30.5C 147.451,17.1972 158.285,8.19716 172.5,3.5 Z"/></g>
<g><path style="opacity:1" fill="#201c1e" d="M 173.5,5.5 C 184.129,4.40695 193.796,6.90695 202.5,13C 206.682,17.015 210.682,21.1817 214.5,25.5C 256.226,97.7859 298.06,170.119 340,242.5C 346.724,253.902 349.891,266.068 349.5,279C 343.923,297.815 331.256,308.148 311.5,310C 223.5,310.667 135.5,310.667 47.5,310C 16.0153,303.874 4.8486,285.374 14,254.5C 56.7472,179.337 99.7472,104.337 143,29.5C 150.175,17.4696 160.342,9.46956 173.5,5.5 Z"/></g>
<g><path style="opacity:1" fill="#f0b822" d="M 142.5,41.5 C 143.525,41.8966 143.692,42.5632 143,43.5C 101.828,113.84 61.1612,184.507 21,255.5C 15.4088,268.926 16.5754,281.592 24.5,293.5C 18.6934,288.041 15.6934,281.207 15.5,273C 15.9007,265.465 17.7341,258.298 21,251.5C 61.2742,181.274 101.774,111.274 142.5,41.5 Z"/></g>
<g><path style="opacity:1" fill="#fbb520" d="M 24.5,293.5 C 16.5754,281.592 15.4088,268.926 21,255.5C 61.1612,184.507 101.828,113.84 143,43.5C 143.692,42.5632 143.525,41.8966 142.5,41.5C 147.888,27.9451 157.221,18.1117 170.5,12C 184.573,8.80187 196.406,12.6352 206,23.5C 209.247,27.6591 212.247,31.9924 215,36.5C 255,105.833 295,175.167 335,244.5C 343.395,256.875 345.729,270.209 342,284.5C 335.445,297.205 324.945,304.039 310.5,305C 223.5,305.667 136.5,305.667 49.5,305C 39.5664,304.363 31.2331,300.529 24.5,293.5 Z"/></g>
<g><path style="opacity:1" fill="#211c1e" d="M 113.5,125.5 C 126.244,123.594 133.577,128.928 135.5,141.5C 133.59,154.232 126.256,159.398 113.5,157C 102.703,150.943 100.203,142.443 106,131.5C 108.114,128.879 110.614,126.879 113.5,125.5 Z"/></g>
<g><path style="opacity:1" fill="#211c1e" d="M 156.5,95.5 C 160.639,94.7042 163.805,96.0375 166,99.5C 166.667,114.833 166.667,130.167 166,145.5C 162.466,150.031 158.632,154.197 154.5,158C 155.936,166.771 160.936,172.438 169.5,175C 178.41,177.788 187.41,178.121 196.5,176C 206.037,172.535 215.704,169.868 225.5,168C 236.304,177.803 246.804,187.97 257,198.5C 258.171,207 254.671,210.166 246.5,208C 238.258,199.255 229.592,191.088 220.5,183.5C 212.53,186.101 204.53,188.601 196.5,191C 194.781,192.87 193.781,195.037 193.5,197.5C 205.245,201.36 216.912,205.527 228.5,210C 238.333,219.833 248.167,229.667 258,239.5C 259.762,248.744 256.262,251.91 247.5,249C 238.47,239.636 229.137,230.636 219.5,222C 208.833,218 198.167,214 187.5,210C 172.057,209.873 157.39,206.54 143.5,200C 136.124,193.971 130.291,186.804 126,178.5C 121.978,182.023 117.811,185.357 113.5,188.5C 112.667,201.487 112.167,214.487 112,227.5C 107.667,232.833 103.333,232.833 99,227.5C 98.3333,212.833 98.3333,198.167 99,183.5C 103.651,178.57 108.484,173.736 113.5,169C 126.066,159.134 138.899,149.634 152,140.5C 152.333,126.833 152.667,113.167 153,99.5C 153.69,97.6498 154.856,96.3164 156.5,95.5 Z"/></g>
<g><path style="opacity:1" fill="#1d1a1e" d="M 154.5,80.5 C 163.762,78.4392 171.262,81.1059 177,88.5C 178.59,90.6498 179.257,92.9832 179,95.5C 174.055,83.1111 165.222,78.9444 152.5,83C 147.786,85.0512 143.619,87.8845 140,91.5C 139.837,89.6133 140.671,88.1133 142.5,87C 146.434,84.5361 150.434,82.3694 154.5,80.5 Z"/></g>
<g><path style="opacity:1" fill="#201d1f" d="M 156.5,86.5 C 164.086,85.8604 169.253,88.8604 172,95.5C 163.667,86.1667 155.333,86.1667 147,95.5C 148.631,91.039 151.798,88.039 156.5,86.5 Z"/></g>
<g><path style="opacity:1" fill="#211d1f" d="M 285.5,222.5 C 289.651,223.486 290.484,225.82 288,229.5C 282.221,234.797 275.721,238.63 268.5,241C 274.741,235.263 280.408,229.097 285.5,222.5 Z"/></g>
<g><path style="opacity:1" fill="#1f1b1d" d="M 309.5,224.5 C 311.527,224.338 313.527,224.505 315.5,225C 316.447,228.791 315.114,231.791 311.5,234C 303.627,236.574 295.627,238.241 287.5,239C 295.009,234.304 302.343,229.47 309.5,224.5 Z"/></g>
<g><path style="opacity:1" fill="#231f21" d="M 92.5,231.5 C 92.56,230.957 92.8933,230.624 93.5,230.5C 99.093,236.179 105.76,238.012 113.5,236C 105.568,239.437 98.5677,237.937 92.5,231.5 Z"/></g>
<g><path style="opacity:1" fill="#201d20" d="M 84.5,229.5 C 88.6353,238.503 95.802,243.17 106,243.5C 110.973,242.903 115.806,242.069 120.5,241C 110.337,245.893 100.337,245.56 90.5,240C 87.0661,237.297 85.0661,233.797 84.5,229.5 Z"/></g>
<g><path style="opacity:1" fill="#1c191c" d="M 291.5,249.5 C 285.974,249.821 280.64,249.488 275.5,248.5C 283.061,246.091 290.728,244.091 298.5,242.5C 300.167,242.667 301.833,242.833 303.5,243C 304.517,244.049 304.684,245.216 304,246.5C 300.199,248.926 296.032,249.926 291.5,249.5 Z"/></g>
<g><path style="opacity:1" fill="#a27a23" d="M 275.5,248.5 C 280.64,249.488 285.974,249.821 291.5,249.5C 285.987,250.816 280.32,250.816 274.5,249.5C 274.624,248.893 274.957,248.56 275.5,248.5 Z"/></g>
<g><path style="opacity:1" fill="#1a181c" d="M 232.5,247.5 C 233.773,248.077 233.773,248.743 232.5,249.5C 220.271,255.974 207.271,259.141 193.5,259C 201.984,258.086 210.317,256.419 218.5,254C 223.618,252.605 228.285,250.438 232.5,247.5 Z"/></g>
<g><path style="opacity:1" fill="#231f21" d="M 243.5,250.5 C 244.773,251.077 244.773,251.743 243.5,252.5C 239.237,256.048 234.404,258.382 229,259.5C 228.5,259 228,258.5 227.5,258C 233.807,257.344 239.141,254.844 243.5,250.5 Z"/></g>
<g><path style="opacity:1" fill="#fec620" d="M 193.5,260.5 C 234.82,261.293 276.153,261.793 317.5,262C 225.167,262.667 132.833,262.667 40.5,262C 91.6683,261.833 142.668,261.333 193.5,260.5 Z"/></g>
<g><path style="opacity:1" fill="#211c1e" d="M 38.5,263.5 C 132.167,263.333 225.834,263.5 319.5,264C 323.409,266.566 324.409,270.066 322.5,274.5C 321.335,275.584 320.002,276.417 318.5,277C 225.5,277.667 132.5,277.667 39.5,277C 33.1887,272.96 32.8553,268.46 38.5,263.5 Z"/></g>
</svg>
 ]])

local w, h = client.screen_size()

local checkboxvelo = ui.new_checkbox("LUA", "A", "velocity")
local colorvelo = ui.new_color_picker("LUA", "A", "velo color", 255, 255, 255, 255)
local dragging = {
    vel_x = ui.new_slider("LUA", "A", "\nX Vel", 0, w, w/2-64),
    vel_y = ui.new_slider("LUA", "A", "\nY Vel", 0, h, 350),
}


local gradient_ranges = {
    {from = 0,  to = 20,  color1 = {180, 40, 70},   color2 = {220, 70, 100}},    
    {from = 20, to = 40,  color1 = {220, 70, 100},  color2 = {240, 120, 100}},    
    {from = 40, to = 60,  color1 = {240, 120, 100}, color2 = {240, 170, 90}},     
    {from = 60, to = 80,  color1 = {240, 170, 90},  color2 = {220, 210, 100}},    
    {from = 80, to = 100, color1 = {220, 210, 100}, color2 = {170, 230, 120}},    
}



local function interpolate_color(percent)
    for _, range in ipairs(gradient_ranges) do
        if percent >= range.from and percent <= range.to then
            local delta = (percent - range.from) / (range.to - range.from)
            local r = math.floor(range.color1[1] + (range.color2[1] - range.color1[1]) * delta)
            local g = math.floor(range.color1[2] + (range.color2[2] - range.color1[2]) * delta)
            local b = math.floor(range.color1[3] + (range.color2[3] - range.color1[3]) * delta)
            return r, g, b
        end
    end
    return 255, 255, 255  -- Default color if out of range
end

local clamp = function(_, value, minimum, maximum)
    return math.min(math.max(value, minimum), maximum)
end

local lerp = function(self, delta, from, to)
    if from == nil then from = 0 end
    if delta > 1 then return to end
    if delta < 0 then return from end
    return from + (to - from) * delta
end

local rectangle_outline = function(x, y, w, h, r, g, b, a, s)
    renderer.rectangle(x, y, w, s, r, g, b, a)
    renderer.rectangle(x, y+h-s, w, s, r, g, b, a)
    renderer.rectangle(x, y+s, s, h-s*2, r, g, b, a)
    renderer.rectangle(x+w-s, y+s, s, h-s*2, r, g, b, a)
end

local smooth_lerp = function(self, time, s, e, no_rounding) 
    if (math.abs(s - e) < 1 or s == e) and not no_rounding then return e end
    local time = self:clamp(globals_frametime() * time * 165, 0.01, 1.0) 
    local value = self:lerp(time, s, e)
    return value 
end

local rounded_rectangle = function(x, y, w, h, r, g, b, a, radius, side)
    y = y + radius
    local data_circle = {
        {x + radius, y, 180},
        side and {} or {x + w - radius, y, 90},
        {x + radius, y + h - radius * 2, 270},
        side and {} or {x + w - radius, y + h - radius * 2, 0},
    }

    local data = {
        {x + radius, y, w - radius * 2, h - radius * 2},
        {x + radius, y - radius, w - radius * 2, radius},
        {x + radius, y + h - radius * 2, w - radius * 2, radius},
        {x, y, radius, h - radius * 2},
        side and {} or {x + w - radius, y, radius, h - radius * 2},
    }

    for _, data in next, data_circle do
        if data ~= nil then
            renderer.circle(data[1], data[2], r, g, b, a, radius, data[3], 0.25)
        end
    end

    for _, data in next, data do
        if data ~= nil then
            renderer.rectangle(data[1], data[2], data[3], data[4], r, g, b, a)
        end
    end
end

local draw_velocity = function(modifier, r, g, b, alpha, x, y)	
    local text_width = renderer.measure_text(nil, ("%s %d%%"):format("Velocity ", modifier*100))
    local iw, ih = warning:measure(nil, 17)
    local rx, ry, rw, rh = x + iw + 30, y + 24, 140, 13






    warning:draw(x - 7, y - 7, nil, 43, 255, 255, 255, 255)

    renderer.text(rx + 1, y + 8, 255, 255, 255, 255, "b", 0, ("%s %d%%"):format("VELOCITY ", modifier * 100))


rounded_rectangle(rx + 2, ry, rw - 2, rh, 16, 16, 16, 180, 4)


rounded_rectangle(rx + 2, ry, math.floor((rw - 3) * modifier), rh, r, g, b, 210, 4)

return iw + rw + 20

end

local velocity_warning = function()
    if not ui.get(checkboxvelo) then return end
    local ent = entity.get_local_player()
    local modifier = entity.get_prop(ent, "m_flVelocityModifier") or 1
    local velocity_percent = modifier * 100
    local r, g, b = interpolate_color(velocity_percent)
    local menu = ui.is_menu_open()
    local x = ui.get(dragging.vel_x)
    local y = ui.get(dragging.vel_y)
    
    if modifier == 1 or not entity.is_alive(ent) then 
        if menu then 
            local w = draw_velocity(0.5, r, g, b, 255, x+3, y+3)
        end
        return 
    end
    
    local w = draw_velocity(modifier, r, g, b, 255, x+3, y+3)
end

client.set_event_callback("paint_ui", velocity_warning)


--==[ Extra Functionalities (добавлено вручную) ]==--

-- Удаление дефолтных хитлогов
client.set_event_callback("player_hurt", function(e)
    return false
end)

-- Динамичный индикатор по yaw
local function get_aa_color()
    local side = ui.get(ui.reference("AA", "Anti-aimbot angles", "Yaw base"))
    if side == "At targets" then return 0,255,0
    elseif side == "Local view" then return 255,0,0
    else return 255,255,0
    end
end

client.set_event_callback("paint", function()
    local r, g, b = get_aa_color()
    renderer.indicator(r, g, b, 255, "IdealYaw")
end)

-- Лог покупок
client.set_event_callback("item_purchase", function(e)
    local buyer = entity.get_player_name(e.userid)
    local item = e.weapon
    client.log(string.format("[BUY] %s купил %s", buyer, item))
end)

-- Лог урона
client.set_event_callback("player_hurt", function(e)
    local attacker = client.userid_to_entindex(e.attacker)
    if attacker == entity.get_local_player() then
        local victim = entity.get_player_name(e.userid)
        client.log(string.format("[HIT] Вы нанесли %d урона по %s", e.dmg_health, victim))
    end
end)

-- Хитшанс ревилер
local hit_chance = ui.reference("Rage", "Aimbot", "Minimum hit chance")
client.set_event_callback("paint_ui", function()
    local hc = ui.get(hit_chance)
    renderer.text(10, 600, 255, 255, 255, 255, "d", 0, "HC: " .. hc .. "%")
end)
