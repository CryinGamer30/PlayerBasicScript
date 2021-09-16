# PlayerBasicScript
Código Para movimiento básico de personaje
public class LogicPlayer : MonoBehaviour

{
    // Variables
    public float SpeedMovement = 2.0f;
    public float RotationSpeed = 200.0f;
    public float JumpForce = 5.0f;
    private Rigidbody Physics;


    // Animacion
    private Animator anim;
    public float x, y;

    // Start is called before the first frame update
    void Start()
    {
        // Codigo Animacion
        anim = GetComponent<Animator>();

        //Esto son fisicas
        Cursor.lockState = CursorLockMode.Locked;
        Cursor.visible = false;
        Physics = GetComponent<Rigidbody>();

    }

    // Update is called once per frame
    void Update()
    {
        //animacion movimineto personaje
        x = Input.GetAxis("Horizontal");
        y = Input.GetAxis("Vertical");
        

        transform.Rotate(0, x * Time.deltaTime * RotationSpeed,0);
        transform.Translate(0, 0, y * Time.deltaTime * SpeedMovement);

        anim.SetFloat("SpeedX", x);
        anim.SetFloat("SpeedY", y);

        //esto es para saltar

        if (Input.GetKeyDown(KeyCode.Space))//esto es para detectar cuando se preciona el espacio y saltar
        {
            Physics.AddForce(new Vector3(0, 5, 0), ForceMode.Impulse);// el 1 es para poder acender
        }
        // aumento de velocidad
        if (Input.GetKeyDown(KeyCode.LeftShift))//esto es para detectar cuando se preciona shift y correr
        {
            SpeedMovement = 5.0f;
        }

        if (Input.GetKeyUp(KeyCode.LeftShift))//esto es para detectar cuando no se esta precionando
        {
            SpeedMovement = 2.0f;
        }


    }
}
