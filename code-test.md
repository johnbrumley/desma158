```c#
using UnityEngine;  
using UnityEngine.AI;  
  
public class SimpleNPC : MonoBehaviour  
{  
    enum NPCState{ WANDER, SLEEP }  
  
    private NPCState currentState;  
  
    public float energy = 10f;  
  
    // wander settings  
    [Header("Wander Settings")]  
    public float lookaheadDistance = 5f;  
    public float wanderAmount = 2f;  
    public float maxDisplacement = 0.4f;  
    public bool showDebugLines = false;  
    private Vector3 lastWanderPoint;  
  
    NavMeshAgent agent;  
  
    void Start()  
    {  
        currentState = NPCState.WANDER;  
  
        agent = GetComponent<NavMeshAgent>();  
    }  
  
    void Update()  
    {  
        switch (currentState)  
        {  
            case (NPCState.WANDER):  
                UpdateWander();  
                break;  
            case (NPCState.SLEEP):  
                UpdateSleep();  
                break;  
        }    
    }  
  
    void UpdateWander()  
    {  
        // make sure we're moving  
        agent.isStopped = false;  
  
        if(lastWanderPoint == null)  
            lastWanderPoint = transform.forward * maxDisplacement;  
  
        // adapted from craig reynolds's wander behavior  
        var newDestination = GetNewWanderDestination(transform.position, transform.forward);  
  
        // check for a valid path (can the agent reach the destination)  
        NavMeshPath path = new NavMeshPath();  
        agent.CalculatePath(newDestination, path);  
        if (path.status != NavMeshPathStatus.PathInvalid)  
        {  
            // valid, so set the destination  
            agent.SetDestination(newDestination);  
        }  
        else  
        {  
            // assume this means I'm at the border, force a turn around  
            newDestination = GetNewWanderDestination(transform.position, -1* transform.forward);  
            agent.SetDestination(newDestination);  
        }  
  
  
        // wandering causes loss of energy  
        energy -= Time.deltaTime;  
        if(energy <= 0)  
        {  
            currentState = NPCState.SLEEP;  
        }  
    }  
  
    Vector3 GetNewWanderDestination(Vector3 start, Vector3 forward)  
    {  
        // calculate next position  
        Vector3 forwardPosition = start + forward * lookaheadDistance;  
  
        // get new random point  
        Vector2 circlePoint = Random.insideUnitCircle.normalized * maxDisplacement;  
        Vector3 randomPoint = new Vector3(circlePoint.x, 0, circlePoint.y);  
  
        // rotate the last point slightly towards the new random point  
        Vector3 newPoint = Vector3.RotateTowards(lastWanderPoint, randomPoint, wanderAmount * Time.deltaTime, maxDisplacement);  
  
        // save the rotated point  
        lastWanderPoint = newPoint;  
  
        // drawing debugs  
        if(showDebugLines)  
        {  
            Debug.DrawLine(start, forwardPosition, Color.white);  
            Debug.DrawLine(start, newPoint + forwardPosition, Color.green);  
        }  
  
        // calc new destination by adding forward and new point  
        return newPoint + forwardPosition;  
    }  
  
    void UpdateSleep()  
    {  
        // stop moving and recover  
        agent.isStopped = true;  
  
        energy += Time.deltaTime;  
  
        if(energy >= 10)  
        {  
            currentState = NPCState.WANDER;  
        }  
    }  
}

```