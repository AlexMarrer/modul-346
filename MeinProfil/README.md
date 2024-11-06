# Meine Person 👦

## **Name**

**Alex Uscata**

## **Arbeitgeber**

**YOO AG**
![YOO AG LOGO](./bilder/YOO-Logo+Claim_RGB.svg)

> Die [YOO AG](https://www.yoo.digital/) arbeitet Projekt orientiert für andere Kunden und erstellt Digitale Lösungen für die Probleme der Kunden

## **Bisherige Erfahrung**

> In der YOO arbeite ich mit Azure in verbindung mit C#. Ich hatte schon paar einige Interne Projekte bei denen ich Azure Functions, Logic Apps oder auch WebApps aufsetzten. Dabei habe ich viel erfahrung mit Azure und dem Graph Client machen können.

## **Programmiersprachen**

Benutzte Programmiersprachen

| Sprache        | Nutzung |
| -------------- | ------- |
| **C#**         | viel    |
| **Java**       | viel    |
| **JavaScript** | viel    |
| **Bash**       | okay    |
| **PHP**        | wenig   |
| **Python**     | wenig   |

Momentan abreite ich am liebsten mit C# oder Java da ich mit Java angefangen habe hänge ich noch sehr daran aber C# überzeugt mich sehr mit der ganzen .NET umgebung

## Interessen

- Programmieren
- Schach
- Fussball

## Hobbies

1. Programmieren
2. Gamen
3. Mit Freunden zu sein

## Was ist mir wichtig

Mit ist wichtig das ich das machen kann was ich machen will.

## Grund für die Ausbildung

Allgemeines Interesse an der Informatik und mein Onkel ist auch Informatiker und war immer so das Gesprächsthema in der Famillie

## Ziele

Ich würde gerne mal studieren die richtung weiss ich noch nicht.

---

# Code 💻

```
public async Task<bool> SetUserBirthday(BirthdayUpdateForum forumData, ILogger log)
{
    var birthDate = new DateTimeOffset(forumData.Date, TimeSpan.Zero).ToUniversalTime();

    Console.WriteLine(birthDate);

    var users = await _graphClient.Users.GetAsync((requestConfiguration) =>
    {
        requestConfiguration.QueryParameters.Select = new string[] { "Id", "UserPrincipalName", "Birthday" };
    });
    var user = users.Value.ToList().FirstOrDefault(u => u.UserPrincipalName.Equals(forumData.Email));

    if (user?.Id == null)
    {
        return false;
    }

    var requestBody = new User
    {
        Birthday = birthDate
    };

    try
    {
        await _graphClient.Users[user.Id].PatchAsync(requestBody);
        return true;
    }
    catch (Exception ex)
    {
        log.LogInformation("----------------------------------------------------");
        log.LogCritical(JsonConvert.SerializeObject(ex));
        log.LogInformation("----------------------------------------------------");
        Console.WriteLine("---");
        Console.WriteLine(ex);
        Console.WriteLine("---");
        throw;
    }
}
```
