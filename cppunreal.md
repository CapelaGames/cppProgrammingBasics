
` UPROPERTY(VisibleAnywhere)`
UProperty macro, which makes it visible inside the Unreal Editor. 

```
	UPROPERTY(VisibleAnywhere)
	UStaticMeshComponent* VisualMesh;
	VisualMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Mesh"));
```

