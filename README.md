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
    {
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
