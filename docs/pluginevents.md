# Broke Protocol Events
> In order for Plugins to add their own functionality to a game, they typically rely on overriding game events. These events are defined as virtual methods within [Events](https://brokeprotocol.com/api/namespace_broke_protocol_1_1_a_p_i.html) and provide a way for Plugins to inject their own custom behavior.

- `[Execution(ExecutionMode.PreEvent)]` -> Executed before other event types. Use this for pre-testing conditions (if you return an optional bool).

- `[Execution(ExecutionMode.Additive)]` -> Default ExecutionMode. Adds your method onto a list of other Plugin methods hooked on the same event.
- `[Execution(ExecutionMode.Override)]` -> Override (disable) any existing Additive or Override hooks on the same event.
- `[Execution(ExecutionMode.Event)]` -> Will always be called on this event (if no previous methods return false). Cannot be Overridden.
- `[Execution(ExecutionMode.PostEvent)]` -> Called after all other Additive, Override, and Event methods. Cannot be overriden.

> In the game's event system, any method can have a bool return type. If a method returns false, it will halt the execution of subsequent methods in the same event chain. This means that if a method in the PreEvent, Additive, Override, or Event ExecutionModes returns false, the PostEvent method will not be executed.

# ManagerEvents
- `virtual bool Start ()`
- `virtual bool Update ()`
- `virtual bool FixedUpdate ()`
- `virtual bool CustomPacket (ConnectData connectData, SvPacket packet)`
- `virtual bool TryLogin (ConnectData connectData)`
- `virtual bool TryRegister (ConnectData connectData)`
- `virtual bool Save ()`
- `virtual bool Load ()`
- `virtual bool ReadGroups ()`
- `virtual bool PlayerLoaded (ConnectData connectData)`
- `virtual bool PrepareMap ()`

# EntityEvents
- `virtual bool Initialize (ShEntity entity)`
- `virtual bool Destroy (ShEntity entity)`
- `virtual bool AddItem (ShEntity entity, int itemIndex, int amount, bool dispatch)`
- `virtual bool RemoveItem (ShEntity entity, int itemIndex, int amount, bool dispatch)`
- `virtual bool Respawn (ShEntity entity)`
- `virtual bool TransferItem (ShEntity entity, byte deltaType, int itemIndex, int amount, bool dispatch)`
- `virtual bool Spawn (ShEntity entity)`
- `virtual bool SecurityTrigger (ShEntity entity, Collider other)`
- `virtual bool NewSector (ShEntity entity, List< Sector > newSectors)`
- `virtual bool SameSector (ShEntity entity)`
- `virtual bool MissileLocked (ShEntity entity, ShThrown missile)`
- `virtual bool SetParent (ShEntity entity, Transform parent)`

# MountableEvents
- `override bool Spawn (ShEntity entity)`

# DestroyableEvents
- `override bool Damage (ShDamageable damageable, DamageIndex damageIndex, float amount, ShPlayer attacker, Collider collider, Vector3 source, Vector3 hitPoint)`
- `virtual bool Death (ShDestroyable destroyable, ShPlayer attacker)`
- `virtual bool DestroySelf (ShDestroyable destroyable)`
- `override bool Spawn (ShEntity entity)`
- `virtual bool Heal (ShDestroyable destroyable, float amount, ShPlayer healer)`

# PhysicalEvents
- `override bool Spawn (ShEntity entity)`

# MovableEvents
- `override bool 	Damage (ShDamageable damageable, DamageIndex damageIndex, float amount, ShPlayer attacker, Collider collider, Vector3 source, Vector3 hitPoint)`
- `override bool 	Death (ShDestroyable destroyable, ShPlayer attacker)`
- `override bool 	Respawn (ShEntity entity)`
- `override bool 	Spawn (ShEntity entity)`

# PlayerEvents
- `override bool Initialize (ShEntity entity)`
- `override bool Destroy (ShEntity entity)`
- `virtual bool Command (ShPlayer player, string message)`
- `virtual bool ChatGlobal (ShPlayer player, string message)`
- `virtual bool ChatLocal (ShPlayer player, string message)`
- `virtual bool ChatVoice (ShPlayer player, byte[] voiceData)`
- `virtual bool SetJob (ShPlayer player, JobInfo newJob, int rank, bool addItems, bool collectCost)`
- `virtual bool SecurityPanel (ShPlayer player, ShApartment apartment)`
- `virtual bool BuyApartment (ShPlayer player, ShApartment apartment)`
- `virtual bool SellApartment (ShPlayer player, ShApartment apartment)`
- `virtual bool Invite (ShPlayer player, ShPlayer other)`
- `virtual bool KickOut (ShPlayer player, ShPlayer other)`
- `override bool Respawn (ShEntity entity)`
- `virtual bool Reward (ShPlayer player, int experienceDelta, int moneyDelta)`
- `virtual bool Collect (ShPlayer player, ShEntity e, bool consume)`
- `virtual bool StopInventory (ShPlayer player, bool sendToSelf)`
- `virtual bool ViewInventory (ShPlayer player, ShEntity searchee, bool force)`
- `virtual bool Kick (ShPlayer player, ShPlayer other, string reason)`
- `virtual bool Ban (ShPlayer player, ShPlayer other, string reason)`
- `override bool AddItem (ShEntity entity, int itemIndex, int amount, bool dispatch)`
- `override bool RemoveItem (ShEntity entity, int itemIndex, int amount, bool dispatch)`
- `virtual bool RemoveItemsDeath (ShPlayer player, bool dropItems)`
- `virtual bool Load (ShPlayer player)`
- `virtual bool Save (ShPlayer player)`
- `virtual bool Injury (ShPlayer player, BodyPart part, BodyEffect effect, byte amount)`
- `virtual bool Restrain (ShPlayer player, ShPlayer initiator, ShRestrained restrained)`
- `virtual bool Unrestrain (ShPlayer player, ShPlayer initiator)`
- `virtual bool ServerInfo (ShPlayer player)`
- `virtual bool DisplayName (ShPlayer player, string username)`
- `virtual bool EnterDoor (ShPlayer player, ShDoor door, ShPlayer sender, bool forceEnter)`
- `virtual bool Follower (ShPlayer player, ShPlayer other)`
- `virtual bool OptionAction (ShPlayer player, int targetID, string id, string optionID, string actionID)`
- `virtual bool SubmitInput (ShPlayer player, int targetID, string id, string input)`
- `virtual bool Ready (ShPlayer player)`
- `virtual bool Point (ShPlayer player, bool pointing)`
- `virtual bool Alert (ShPlayer player)`
- `virtual bool MinigameFinished (ShPlayer player, bool successful, int targetID, string id, string optionID)`
- `override bool DestroySelf (ShDestroyable destroyable)`
- `override bool TransferItem (ShEntity entity, byte deltaType, int itemIndex, int amount, bool dispatch)`
- `virtual bool MenuClosed (ShPlayer player, string id)`
- `virtual bool Park (ShPlayer player, ShTransport transport)`
- `virtual bool VideoPanel (ShPlayer player, ShEntity entity)`
- `virtual bool TextPanelButton (ShPlayer player, string id, string optionID)`
- `virtual bool SetEquipable (ShPlayer player, ShEquipable equipable)`
- `virtual bool CrackStart (ShPlayer player, int entityID)`
- `virtual bool Mount (ShPlayer player, ShMountable mount, byte seat)`
- `virtual bool Dismount (ShPlayer player)`
- `override bool Spawn (ShEntity entity)`
- `virtual bool PlaceItem (ShPlayer player, ShEntity placeableEntity, Vector3 position, Quaternion rotation, float spawnDelay)`
- `virtual bool ResetAI (ShPlayer player)`
- `virtual bool SetWearable (ShPlayer player, ShWearable wearable)`
- `virtual bool RestrainOther (ShPlayer player, ShPlayer hitPlayer, ShRestraint restraint)`
- `virtual bool Deposit (ShPlayer player, int entityID, int amount)`
- `virtual bool Withdraw (ShPlayer player, int entityID, int amount)`
- `virtual bool TryGetJob (ShPlayer player, ShPlayer employer)`
- `virtual bool Bomb (ShPlayer player, ShVault vault)`
- `virtual bool Repair (ShPlayer player, ShTransport transport)`
- `virtual bool Lockpick (ShPlayer player, ShTransport transport)`
- `virtual bool Consume (ShPlayer player, ShConsumable consumable, ShPlayer healer)`
- `virtual bool TransferShop (ShPlayer player, byte deltaType, int itemIndex, int amount)`
- `virtual bool TransferTrade (ShPlayer player, byte deltaType, int itemIndex, int amount)`
- `override bool NewSector (ShEntity entity, List< Sector > newSectors)`
- `override bool SameSector (ShEntity entity)`
- `virtual bool Fire (ShPlayer player)`
- `override bool SetParent (ShEntity entity, Transform parent)`
- `override bool Damage (ShDamageable damageable, DamageIndex damageIndex, float amount, ShPlayer attacker, Collider collider, Vector3 source, Vector3 hitPoint)`
- `override bool Death (ShDestroyable destroyable, ShPlayer attacker)`
- `virtual bool UpdateTextDisplay (ShPlayer player, ShTextDisplay textDisplay)`