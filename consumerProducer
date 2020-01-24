

import java.util.concurrent.ArrayBlockingQueue;

class Buffer{
    ArrayBlockingQueue<Integer> array = new ArrayBlockingQueue<Integer>(5);
    int num;
    boolean set = false;
    public synchronized void add(int num){
        if(array.size() == 5){
            set = true;
            notify();
        }
        while(set){
            try{
                wait();
                notify();
            }catch (Exception e){

            }
        }
        System.out.println("Adding value: " + num);
        this.num = num;
        this.array = array;
        array.add(num);
        System.out.println("IN the Array " + array);
    }
    public synchronized void get(){

        if(array.size() == 0){
            set = false;
            notify();
        }
        while(!set){
            try{
                wait();
            }catch (Exception e){

            }
        }
        num = array.remove();
        System.out.println("Getting value: " + num);
    }
}

class producer implements Runnable{
    Buffer num;
    public producer( Buffer num){
        this.num = num;
        Thread producer = new Thread(this, "producer");
        producer.start();
    }
    @Override
    public void run() {
        int i = 0;
        while(true){
            num.add(i++);
            try{
                Thread.sleep(500);
            }catch ( Exception e){

            }
        }

    }
}

class consumer implements Runnable{
    Buffer num;
    public consumer( Buffer num){
        this.num = num;
        Thread consumer = new Thread(this, "consumer");
        consumer.start();
    }
    @Override
    public void run() {
        while(true){
            num.get();
            try{
                Thread.sleep(500);
            }catch ( Exception e){

            }
        }

    }
}
public class Project1OS {
    public static void main(String[] args){
        Buffer num = new Buffer();
        new producer(num);
        new consumer(num);
    }
}
