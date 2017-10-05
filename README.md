# design-patterns-java

Behaviour patterns

1. Observer

import java.util.ArrayList;
import java.util.List;

interface Observable {
    void addObserver(Observer observer);
    void removeObsearver(Observer observer);
    void notifyAllObservers();
}


class Car implements Observable {
    private List<Observer> observers = new ArrayList();
    private int currentPrice;
    private int oldPrice;
    
    public void setPrice(int newPrice) {
        oldPrice = currentPrice;
        currentPrice = newPrice;
        
        notifyAllObservers();
    }
    
  public void addObserver(Observer observer){
        if (!observers.contains(observer)) {
            observers.add(observer);
        }
    }
    
   public  void removeObsearver(Observer observer){
        observers.remove(observer);
    }
    
   public  void notifyAllObservers(){
        for (Observer observer : observers ) {
            observer.update(oldPrice, currentPrice);
        }
    }
}


     interface Observer {
         void update(int currentPrice, int newPrice);
        
     }

 class User implements Observer{
    private  Observable observable;
    private String name;
     
     public User(Observable observable, String name) {
         observable = observable;
         this.name = name;
         
         observable.addObserver(this);
     }

     public void update(int currentPrice, int newPrice) {
         System.out.println( "NAME: " + name+ "\nOld price: " + currentPrice + " \nCurrent price: " + newPrice);
     }
 }
 
 
 public class MainClass {
     
     public static void main(String [] args) {
         Car car = new Car();
         
         User user1 = new User(car,"USER1");
         User user2 = new User(car,"USER2");
         User user3 = new User(car,"USER3");
         
         car.setPrice(5000);
         car.setPrice(10000);


     }
 }
