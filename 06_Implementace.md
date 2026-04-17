
Jsou zde různe ukázky jak jsem implementovali do naší hry mechaniky.



Movement:

```
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

public class CreateWaypoint : MonoBehaviour
{

    // public static CreateWaypoint Instance;
    // [SerializeField] private Vector3 YRoomVal;
    // [SerializeField] private GameObject PlayerWaypoint;
    private GameObject NewPlayerWaypoint;
    public GameObject AbnoParent;
    public GameObject EmployeeParent;

    // private void Awake()
    // {
    //     Instance = this;
    // }


    public void RoomWaypointUI()
        {
           // if (GameObject.FindWithTag("WaypointUI"))
            //{
                // Prozatim1.SetActive(true);
                
            //}
        }


    public void SetPlayerWaypoint(GameObject playerWaypoint)
    {

        NewPlayerWaypoint = playerWaypoint;
     
    }
    public void CreateWaypointUI(float YRoomVal)
    {
        Vector3 mousePos = Input.mousePosition;

        Vector3 worldPos = Camera.main.ScreenToWorldPoint(mousePos);

        if(NewPlayerWaypoint != null){
        NewPlayerWaypoint.transform.position = new Vector3(worldPos.x, YRoomVal ,0) ; // tady byl worldPos.y predtim na y

        NewPlayerWaypoint = null;
        }

        
    }
    public void CreateAbnoParent(GameObject Parent)
    {
        AbnoParent = Parent;
    }
    public void CreateAttackWaypoint()
    {
        if(NewPlayerWaypoint != null)
        {
            
            NewPlayerWaypoint.transform.parent = AbnoParent.transform;
            NewPlayerWaypoint.transform.localPosition = new Vector3(0, 0 ,0) ;
            NewPlayerWaypoint = null;
            AbnoParent = null;
        }
    }
    public void ReturnWaypoints(GameObject Waypoint)
    {
        Waypoint.transform.parent = EmployeeParent.transform;
    }
}

```





https://github.com/user-attachments/assets/f751a39f-883c-4a6b-9bb4-ec01b2c720de






Abnormality Attack // Employee Attack/Hurt Animation:




https://github.com/user-attachments/assets/ca90735a-f971-4232-816d-4d7ff466d520


Employee Attack command (Follow Enemy):

https://github.com/user-attachments/assets/a7ba0157-e17f-40ef-b0a4-fce35446982d




[replay_preview.wav](https://github.com/user-attachments/files/26335346/replay_preview.wav)




Ukazka skeletona a riggingu Nugetky:


<img width="330" height="688" alt="image" src="https://github.com/user-attachments/assets/0ed25fe9-59a0-4fd1-a409-647c74bfa0c9" />
<img width="330" height="687" alt="image" src="https://github.com/user-attachments/assets/cebfd766-c33a-401d-a97a-15f64d152334" />
<img width="330" height="697" alt="image" src="https://github.com/user-attachments/assets/2d0fedb0-1131-43ca-b850-6f7d3f275759" />

Audio:
Kod který na zavolání změní ost pomocí fadingu 
```
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

public class AudioManager : MonoBehaviour
{

    private bool isPlayingTrack01;

    public static AudioManager instance;
    private AudioSource track01, track02;
    
    public AudioClip defaultAmbiance;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Awake()
    {
        if (instance == null)
        {
            instance = this;
        }

    }

    public void SwapTrack(AudioClip newClip)
    {
        StopAllCoroutines();
        StartCoroutine(FadeTrack(newClip));
        isPlayingTrack01 = !isPlayingTrack01;
    }



    private void Start()
    {
        track01 = gameObject.AddComponent<AudioSource>();
        track01.loop = true;
        track02 = gameObject.AddComponent<AudioSource>();
        track02.loop = true;
        isPlayingTrack01 = true;

        SwapTrack(defaultAmbiance);
    }

    public void ReturnToDefault()
    {
        SwapTrack(defaultAmbiance);
    }
    private IEnumerator FadeTrack(AudioClip newClip)
    {
        float timeToFade = 1.25f;
        float timeElapsed = 0;
        if (isPlayingTrack01)
        {
            track02.clip = newClip;
            track02.Play();
            while(timeElapsed < timeToFade)
            {
                track02.volume = Mathf.Lerp(0,1,timeElapsed/timeToFade);
                track01.volume = Mathf.Lerp(1,0,timeElapsed/timeToFade);
                timeElapsed += Time.deltaTime;
                yield return null;
            }
            track01.Stop();
        }
        else
        {
            track01.clip = newClip;
            track01.Play();
                        while(timeElapsed < timeToFade)
            {
                track02.volume = Mathf.Lerp(1,0,timeElapsed/timeToFade);
                track01.volume = Mathf.Lerp(0,1,timeElapsed/timeToFade);
                timeElapsed += Time.deltaTime;
                yield return null;
            }
            track02.Stop();
        }
    }

}

```
