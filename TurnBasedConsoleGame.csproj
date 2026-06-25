using System;

public class Player
{
    public string Name { get; set; }
    public int Health { get; set; }
    public bool IsAlive { get; set; }
    public bool IsHuman { get; set; }

    public Attack QuickAttack { get; }
    public Attack HeavyAttack { get; }
    public Attack PreciseAttack { get; }

    private static readonly Random rnd = new Random();

    public Player(string name, int health, bool isHuman)
    {
        Name = name;
        Health = health;
        IsAlive = health > 0;
        IsHuman = isHuman;

        QuickAttack = new Attack("Quick Attack", 10, 95, 10);
        HeavyAttack = new Attack("Heavy Attack", 30, 55, 20);
        PreciseAttack = new Attack("Precise Attack", 15, 100, 5);
    }

    public void DecideAction(Player opponent)
    {
        string input;

        if (IsHuman)
        {
            Console.WriteLine("1: Quick Attack");
            Console.WriteLine("2: Heavy Attack");
            Console.WriteLine("3: Precise Attack");
            Console.WriteLine("4: Heal");

            input = Console.ReadLine() ?? "";
        }
        else
        {
            input = rnd.Next(1, 5).ToString();
        }

        switch (input)
        {
            case "1":
                QuickAttack.Execute(this, opponent);
                break;

            case "2":
                HeavyAttack.Execute(this, opponent);
                break;

            case "3":
                PreciseAttack.Execute(this, opponent);
                break;

            case "4":
                Heal();
                break;

            default:
                Console.WriteLine("Invalid action.");
                break;
        }
    }

    public void Heal()
    {
        if (!IsAlive)
        {
            return;
        }

        int heal = rnd.Next(10, 21);
        Health += heal;

        if (Health > 100)
        {
            Health = 100;
        }

        Console.WriteLine(Name + " got healed by " + heal + " HP.");
        Console.WriteLine(Health + " HP left");
    }
}

public class Attack
{
    private static readonly Random random = new Random();

    public string Name { get; }
    public int Damage { get; }
    public int HitChance { get; }
    public int CriticalChance { get; }

    public Attack(string name, int damage, int hitChance, int criticalChance)
    {
        Name = name;
        Damage = damage;
        HitChance = hitChance;
        CriticalChance = criticalChance;
    }

    public void Execute(Player attacker, Player target)
    {
        int hitRoll = random.Next(1, 101);

        if (hitRoll > HitChance)
        {
            Console.WriteLine(attacker.Name + " used " + Name + ", but missed!");
            return;
        }

        int finalDamage = Damage;

        int criticalRoll = random.Next(1, 101);

        if (criticalRoll <= CriticalChance)
        {
            finalDamage *= 2;
            Console.WriteLine("Critical Hit!");
        }

        target.Health -= finalDamage;

        if (target.Health <= 0)
        {
            target.Health = 0;
            target.IsAlive = false;
        }

        Console.WriteLine(attacker.Name + " used " + Name + " and dealt " + finalDamage + " damage.");
        Console.WriteLine(target.Name + " has " + target.Health + " HP left.");
    }
}

public class Program
{
    public static string InputName(string input, bool firstPlayer)
    {
        if (string.IsNullOrWhiteSpace(input) && firstPlayer)
        {
            return "Parry Hotter";
        }
        else if (string.IsNullOrWhiteSpace(input) && !firstPlayer)
        {
            return "Randalf";
        }
        else
        {
            return input;
        }
    }

    public static void Main()
    {
        Console.WriteLine("First name:");
        string inputOne = Console.ReadLine();

        Console.WriteLine("Second name:");
        string inputTwo = Console.ReadLine();

        inputOne = InputName(inputOne, true);
        inputTwo = InputName(inputTwo, false);

        Player playerOne = new Player(inputOne, 100, true);
        Player playerTwo = new Player(inputTwo, 100, false);

        int round = 1;

        while (playerOne.IsAlive && playerTwo.IsAlive)
        {
            Console.WriteLine("------ Round: " + round + " ------");

            if (playerOne.IsAlive)
            {
                playerOne.DecideAction(playerTwo);
            }

            if (playerTwo.IsAlive)
            {
                playerTwo.DecideAction(playerOne);
            }

            round++;
        }

        Console.WriteLine("------ END ------");

        if (!playerOne.IsAlive)
        {
            Console.WriteLine(playerOne.Name + " died. RIP.");
        }
        else
        {
            Console.WriteLine(playerTwo.Name + " died. RIP.");
        }
    }
}
