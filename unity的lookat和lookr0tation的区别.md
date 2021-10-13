# Unity的LookAt和LookRotation的区别

[网页]: https://blog.csdn.net/zhh9426/article/details/78895703

```c#
using UnitEngine;

public Class LookAt:MonoBehaviour
{
    private Camera _camera;
    public GameObject UIText;
    
    private void Awake()
    {
        //绑定主摄像机
        _camera = Camera.main;
    }
    void Start()
    {
        if(_camera == null)
        {
           return; 
        }
    }
    
    void Update()
    {
        //使用LookAt，默认Z轴正方向指向摄像机
        UIText.transform.LookAt(_camera.transform.position);
        
        //使用LookRotation
        //计算一个向量
        Vector3 v =UIText.transform.position - _camera.transfrom.position;
        //目标的Z轴指向向量的方向
        UIText.transform.rotation = Quaternion.LookRotation(v);
    }
    
    //画线的方法
    private void OnDrawGizmos()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawLine(UIText.transform.position, _camera.transfrom.position);
        //或者
        Debug.DrawLine(UIText.transform.position,_camera.transfrom.position,color red);
        
    }
}
```

