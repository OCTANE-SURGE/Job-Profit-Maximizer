import java.util.*;
class Job {
    char id;
    int deadline;
    int profit;

    public Job(char id, int deadline, int profit) {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }
}
public class JobProfitMaximizer {
    public void scheduleJobs(List<Job> jobs) {
        Collections.sort(jobs, (a, b) -> b.profit - a.profit);
        int n = jobs.size();
        int maxDeadline = 0;
        for (Job job : jobs) {
            maxDeadline = Math.max(maxDeadline, job.deadline);
        }

        char[] result = new char[maxDeadline];
        boolean[] slots = new boolean[maxDeadline];

        int totalProfit = 0;

        for (Job job : jobs) {
            for (int j = Math.min(maxDeadline, job.deadline) - 1; j >= 0; j--) {
                if (!slots[j]) {
                    slots[j] = true;
                    result[j] = job.id;
                    totalProfit += job.profit;
                    break;
                }
            }
        }
        System.out.println("Scheduled Jobs: " + Arrays.toString(result));
        System.out.println("Total Maximum Profit: " + totalProfit);
    }
    public static void main(String[] args) {
        List<Job> jobs = new ArrayList<>();
        jobs.add(new Job('A', 2, 100));
        jobs.add(new Job('B', 1, 19));
        jobs.add(new Job('C', 2, 27));
        jobs.add(new Job('D', 1, 25));
        jobs.add(new Job('E', 3, 15));

        JobProfitMaximizer maximizer = new JobProfitMaximizer();
        maximizer.scheduleJobs(jobs);
    }
}
