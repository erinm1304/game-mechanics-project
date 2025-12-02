# game-mechanics-project[BeaverNPC.cs](https://github.com/user-attachments/files/23884902/BeaverNPC.cs)
using UnityEngine;
using TMPro;
using UnityEngine.UI;
using System.Collections;

public class BeaverDialogue : MonoBehaviour
{
    [Header ("UI")]
    public CanvasGroup dialoguePanel;      
    public TextMeshProUGUI dialogueText;   
    public GameObject pressEIndicator;     

    private bool playerInRange = false;
    private bool isTalking = false;

    private void Start()
    {
        dialoguePanel.alpha = 0;
        dialoguePanel.gameObject.SetActive(true);
        pressEIndicator.SetActive(false);
    }

    private void Update()
    {[BeaverNPC.cs](https://github.com/user-attachments/files/23884936/BeaverNPC.cs)[BridgeFixSequence.cs](https://github.com/user-attachments/files/23884937/BridgeFixSequence.cs)[WoodsIntroCutscene.cs](https://github.com/user-attachments/files/23884959/WoodsIntroCutscene.cs)
[ThornScript.cs](https://github.com/user-attachments/files/23884958/ThornScript.cs)
[RunOffScreen.cs](https://github.com/user-attachments/files/23884957/RunOffScreen.cs)
[PoppyFollowButterfly.cs](https://github.com/user-attachments/files/23884956/PoppyFollowButterfly.cs)
[poopyMovements.cs](https://github.com/user-attachments/files/23884955/poopyMovements.cs)
[PlayerInventory.cs](https://github.com/user-attachments/files/23884954/PlayerInventory.cs)
[PlayerHealth.cs](https://github.com/user-attachments/files/23884953/PlayerHealth.cs)
[ItemPickup.cs](https://github.com/user-attachments/files/23884952/ItemPickup.cs)
[HealthUI.cs](https://github.com/user-attachments/files/23884951/HealthUI.cs)
[HealthSystem.cs](https://github.com/user-attachments/files/23884950/HealthSystem.cs)
[GardenExitCutscene.cs](https://github.com/user-attachments/files/23884949/GardenExitCutscene.cs)
[GameManager.cs](https://github.com/user-attachments/files/23884948/GameManager.cs)
[DialogueTrigger.cs](https://github.com/user-attachments/files/23884946/DialogueTrigger.cs)
[dialogueManager.cs](https://github.com/user-attachments/files/23884945/dialogueManager.cs)
[DialogueLine.cs](https://github.com/user-attachments/files/23884944/DialogueLine.cs)
[DamageFlash.cs](https://github.com/user-attachments/files/23884943/DamageFlash.cs)
[CollarPickup.cs](https://github.com/user-attachments/files/23884942/CollarPickup.cs)
[CoinScript.cs](https://github.com/user-attachments/files/23884941/CoinScript.cs)
[ButterflyPath.cs](https://github.com/user-attachments/files/23884940/ButterflyPath.cs)
[ButterflyOffset.cs](https://github.com/user-attachments/files/23884939/ButterflyOffset.cs)
[ButterflyMovements.cs](https://github.com/user-attachments/files/23884938/ButterflyMovements.cs)


        if (playerInRange && !isTalking && Input.GetKeyDown(KeyCode.E))
        {
            StartCoroutine(StartDialogue());
        }
    }

    private IEnumerator StartDialogue()
    {
        isTalking = true;
        pressEIndicator.SetActive(false);

        // Fade panel in
        yield return StartCoroutine(FadeCanvasGroup(dialoguePanel, 0, 1, 0.3f));

        dialogueText.text = "Hey Poppy! The bridge is broken. I can fix it if you find me 3 sticks!";

        yield return new WaitForSeconds(3f);

        // Fade panel out
        yield return StartCoroutine(FadeCanvasGroup(dialoguePanel, 1, 0, 0.3f));

        isTalking = false;
    }

    private IEnumerator FadeCanvasGroup(CanvasGroup cg, float start, float end, float time)
    {
        float t = 0;
        while (t < time)
        {
            t += Time.deltaTime;
            cg.alpha = Mathf.Lerp(start, end, t / time);
            yield return null;
        }
        cg.alpha = end;
    }

    private void OnTriggerEnter2D(Collider2D col)
    {
        if (col.CompareTag("Player"))
        {
            playerInRange = true;
            pressEIndicator.SetActive(true);
        }
    }

    private void OnTriggerExit2D(Collider2D col)
    {
        if (col.CompareTag("Player"))
        {
            playerInRange = false;
            pressEIndicator.SetActive(false);
        }
    }
}
