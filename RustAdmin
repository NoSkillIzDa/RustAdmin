using Oxide.Core.Libraries.Covalence;

namespace Oxide.Plugins
{
    [Info("RustAdmin", "NoSkill_IzDa", "1.0.0")]
    [Description("Plugin to kick players with a command and reason.")]

    public class RustAdmin : CovalencePlugin
    {
        private const string PermissionKick = "rustadmin.kick";

        void Init()
        {
            permission.RegisterPermission(PermissionKick, this);
        }

        [Command("kick", "rustadmin.kick")]
        private void KickCommand(IPlayer player, string command, string[] args)
        {
            if (!player.HasPermission(PermissionKick))
            {
                player.Reply(lang.GetMessage("NoPermission", this, player.Id));
                return;
            }

            if (args.Length < 1)
            {
                player.Reply(lang.GetMessage("Usage", this, player.Id));
                return;
            }

            var target = players.FindPlayer(args[0]);
            if (target == null || !target.IsConnected)
            {
                player.Reply(lang.GetMessage("PlayerNotFound", this, player.Id));
                return;
            }

            var reason = args.Length > 1 ? string.Join(" ", args.Skip(1)) : lang.GetMessage("DefaultReason", this, player.Id);
            target.Kick(reason);
            player.Reply(string.Format(lang.GetMessage("PlayerKicked", this, player.Id), target.Name, reason));
        }

        protected override void LoadDefaultMessages()
        {
            lang.RegisterMessages(new Dictionary<string, string>
            {
                ["NoPermission"] = "You do not have permission to use this command.",
                ["Usage"] = "Usage: /kick \"player\" [reason]",
                ["PlayerNotFound"] = "Player not found or not online.",
                ["DefaultReason"] = "No reason provided.",
                ["PlayerKicked"] = "You kicked {0} for: {1}"
            }, this);

            lang.RegisterMessages(new Dictionary<string, string>
            {
                ["NoPermission"] = "Du hast keine Berechtigung, diesen Befehl zu verwenden.",
                ["Usage"] = "Verwendung: /kick \"spieler\" [grund]",
                ["PlayerNotFound"] = "Spieler nicht gefunden oder nicht online.",
                ["DefaultReason"] = "Kein Grund angegeben.",
                ["PlayerKicked"] = "Du hast {0} gekickt für: {1}"
            }, this, "de");
        }
    }
}
