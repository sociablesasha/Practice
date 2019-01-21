# [17] N + 1 (fetch & join)

## 정의
* 1번의 쿼리로 100개의 데이터를 가져와야 하는 경우
* N번의 추가 쿼리가 발생하는 문제


## 이유
1. cat 테이블 전체 조회 (200건 리턴)
2. cat 데이터 200건을 각각 영속화 진행
3. cat 엔티티의 owner 속성이 즉시 로딩으로 되어 있기에 owner 데이터를 가져오기 위한 쿼리


## Code
```java
@Slf4j
@RunWith(SpringRunner.class)
@SpringBootTest
public class NPlusOneProblem {    
 
    @Autowired
    private OrderRepository orderRepository;
 
    @PersistenceContext
    private EntityManager em;
   
 
    private void makeTestData() {
 
        int orderProductId = 0;
        for (int i = 0; i < 10; i++) {
            Shipping shipping = new Shipping();
            shipping.setId(i);
 
            Order order = new Order();
            order.setId(i);
            order.setShipping(shipping);
 
            for (int j = 0; j < 5; j++) {
                OrderProduct orderProduct = new OrderProduct();
                orderProduct.setId(orderProductId);
                orderProduct.setOrder(order);
                orderProductId++;
            }
 
            em.persist(order);
        }
 
        em.flush();
        em.clear();
    }
    
    
    @Test
    @Transactional
    public void OneToOne쿼리_fetch적용하지않음() {
        makeTestData();
 
        TypedQuery typedQuery = em.createQuery("select o from Order o left join o.shipping", Order.class);
        List<Order> orderList = typedQuery.getResultList();
        assertThat(10, is(orderList.size()));
 
        Order order = em.find(Order.class, 8);
        assertNotNull(order);
    }
 
    @Test
    @Transactional
    public void OneToOne쿼리_fetch적용() {
        makeTestData();
 
        TypedQuery typedQuery = em.createQuery("select o from Order o left join fetch o.shipping", Order.class);
        List<Order> orderList = typedQuery.getResultList();
        assertThat(10, is(orderList.size()));
 
        Order order = em.find(Order.class, 8);
        assertNotNull(order);
    }
 
    /**
     * Order 테이블에 데이터 10개
     * OrderProducts 테이블에 데이터 5개
     * 위의 두 개의 테이블을 서로 조인하면 50개가 나온다.
     */
    @Test
    @Transactional
    public void fetch적용시_데이터가_중복노출되는현상() {
        makeTestData();
 
        TypedQuery typedQuery = em.createQuery("select o from Order o left join fetch o.orderProducts", Order.class);
        System.out.println("--------------------------------------------");
        List<Order> orderList = typedQuery.getResultList();
        System.out.println("--------------------------------------------");
 
        assertThat(10, is(not(orderList.size())));
        assertThat(50, is(orderList.size()));
    }
 
    @Test
    @Transactional
    public void fetch적용시_데이터가_중복노출되는현상_distinct로_해결하기() {
        makeTestData();
 
        TypedQuery typedQuery = em.createQuery("select distinct o from Order o join fetch o.orderProducts", Order.class);
        System.out.println("--------------------------------------------");
        List<Order> orderList = typedQuery.getResultList();
        System.out.println("--------------------------------------------");
 
        assertThat(10, is(orderList.size()));
    }
}
 
interface OrderRepository extends JpaRepository<Order, Integer> {
}
 
 
@Getter
@Setter
@NoArgsConstructor
@lombok.ToString
@Entity
@Table(name = "NPLUS_ORDER")
class Order {
    @Id
    private int id;
 
    @OneToOne(fetch = FetchType.LAZY, mappedBy = "order", cascade = CascadeType.PERSIST, optional = false)
    private Shipping shipping;
 
    @OneToMany(fetch = FetchType.LAZY, mappedBy = "order", cascade = CascadeType.PERSIST)
    private List<OrderProduct> orderProducts = new ArrayList<>();
 
    public void setShipping(Shipping shipping) {
        this.shipping = shipping;
        shipping.setOrder(this);
    }
 
    public void addOrderProducts(OrderProduct orderProduct) {
        orderProducts.add(orderProduct);
    }
}
 
 
@Getter
@Setter
@NoArgsConstructor
@lombok.ToString(exclude = "order")
@Entity
@Table(name = "NPLUS_SHIPPING")
class Shipping {
 
    @Id
    private int id;
 
    @OneToOne(fetch = FetchType.LAZY, optional = false)
    private Order order;
}
 
 
@Getter
@Setter
@NoArgsConstructor
@lombok.ToString(exclude = "order")
@Entity
@Table(name = "NPLUS_ORDER_PRODUCT")
class OrderProduct {
 
    @Id
    private int id;
 
    @ManyToOne(fetch = FetchType.LAZY)
    private Order order;
 
    public void setOrder(Order order) {
        this.order = order;
        order.addOrderProducts(this);
    }
}
```
