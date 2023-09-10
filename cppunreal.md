
` UPROPERTY(VisibleAnywhere)` \n
UProperty macro, which makes it visible inside the Unreal Editor. 

```
	UPROPERTY(VisibleAnywhere)
	UStaticMeshComponent* VisualMesh;
	VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh"));
```
Create a Mesh

`VisualMesh->SetupAttachment(RootComponent);`
Attach to RootComponent.

```
static ConstructorHelpers::FObjectFinder<UStaticMesh> CubeVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Cube.Shape_Cube"));

if (CubeVisualAsset.Succeeded())
{
    VisualMesh->SetStaticMesh(CubeVisualAsset.Object);
    VisualMesh->SetRelativeLocation(FVector(0.0f, 0.0f, 0.0f));
}
```

` Tick(float DeltaTime)`
Similar to update, called every frame

`BeginPlay()`
Similar to start, called when the game starts or when spawned

